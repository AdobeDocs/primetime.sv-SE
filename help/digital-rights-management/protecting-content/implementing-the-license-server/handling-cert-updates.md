---
title: Hantera certifikatuppdateringar när certifikat som utfärdas av Adobe upphör att gälla
description: Hantera certifikatuppdateringar när certifikat som utfärdas av Adobe upphör att gälla
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Hantera certifikatuppdateringar när certifikat som utfärdas av Adobe upphör{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Du kan behöva skaffa ett nytt certifikat från Adobe. Ett produktionscertifikat upphör till exempel att gälla när ett utvärderingscertifikat upphör att gälla eller när du växlar från en utvärdering till ett produktionscertifikat. När ett certifikat upphör att gälla och du inte vill paketera om innehållet som använder det gamla certifikatet, kan du göra licensservern medveten om både det gamla och nya certifikatet.

Så här uppdaterar du en server med nya certifikat:

1. (Valfritt) När du lägger till nya poster i en befintlig DRM-principuppdateringslista eller återkallningslista måste du signera med de nya inloggningsuppgifterna och använda det gamla certifikatet för att validera signaturen i den befintliga filen.

   Du kan till exempel använda följande kommandorad för att lägga till en post i en befintlig DRM-principuppdateringslista som har signerats med en annan autentiseringsuppgift:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Valfritt) Använd Java API för att uppdatera licensservern med den nya uppdateringslistan eller listan över återkallade DRM-principer:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   eller:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   I referensimplementeringen är de egenskaper som du använder `HandlerConfiguration.RevocationList` och `HandlerConfiguration.PolicyUpdateList`. Du måste också uppdatera certifikatet som används för att verifiera signaturerna: `RevocationList.verifySignature.X509Certificate`.

1. Uppdatera licensservern med nya och gamla certifikat.

   Om du vill förbruka innehåll som har paketerats med de gamla certifikaten måste du se till att licensservern har tillgång till den gamla och nya licensserverns autentiseringsuppgifter samt transportautentiseringsuppgifter.

   För autentiseringsuppgifter för licensservern:

   * Kontrollera att den aktuella autentiseringsuppgiften skickas till konstruktorn `LicenseHandler`:

      * I referensimplementeringen anger du den med egenskapen `LicenseHandler.ServerCredential`.
      * I Adobe Primetime DRM Server for Protected Streaming måste den aktuella autentiseringsuppgiften vara den första autentiseringsuppgiften som anges i `LicenseServerCredential`-elementet i filen flashaccess-tenant.xml.
   * Kontrollera att aktuella och gamla autentiseringsuppgifter anges till `AsymmetricKeyRetrieval`

      * I referensimplementeringen anger du den med egenskaperna `LicenseHandler.ServerCredential` och `AsymmetricKeyRetrieval.ServerCredential. n`.

      * I Primetimes DRM-server för skyddad direktuppspelning anges de gamla autentiseringsuppgifterna efter den första autentiseringsuppgiften i `LicenseServerCredential`-elementet i filen flashaccess-tenant.xml.

   För transportinloggningsuppgifterna:

   * Kontrollera att de aktuella autentiseringsuppgifterna skickas till metoden `HandlerConfiguration.setServerTransportCredential()`:

      * I referensimplementeringen anger du den med egenskapen `HandlerConfiguration.ServerTransportCredential`.
      * I Primetime DRM-servern för skyddad direktuppspelning måste den aktuella autentiseringsuppgiften vara den första autentiseringsuppgiften som anges i `TransportCredential`-elementet i [!DNL flashaccess-tenant.xml]-filen.
   * Kontrollera att de gamla autentiseringsuppgifterna har angetts för `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * I referensimplementeringen anger du den med egenskaperna `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * I Primetimes DRM-server för skyddad direktuppspelning anges detta efter den första autentiseringen i `TransportCredential`-elementet i filen flashaccess-tenant.xml.




1. Uppdatera paketeringsverktygen för att se till att de paketerar innehåll med de aktuella inloggningsuppgifterna. Kontrollera att det senaste licensservercertifikatet, transportcertifikatet och paketerarens autentiseringsuppgifter används för paketering.
1. Uppdatera nyckelserverns licensservercertifikat enligt följande:

   * Uppdatera inloggningsuppgifterna i Adobe Primetime DRM Key Server-klientkonfigurationsfilen genom att ta med både den gamla och den nya inloggningsuppgifterna för Key Server i flashaccess-keyserver-tenant.xml.
   * Kontrollera att det aktuella certifikatet skickas till metoden `HandlerConfiguration.setKeyServerCertificate()`.

      * I referensimplementeringen anger du den med egenskapen `HandlerConfiguration.KeyServerCertificate`.
      * I Primetime DRM-servern för skyddad direktuppspelning anger du nyckelserverns certifikat i genom elementet Configuration/Tenant/Certificates/KeyServer.

