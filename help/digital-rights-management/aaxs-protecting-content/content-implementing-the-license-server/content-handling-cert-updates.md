---
seo-title: Hantera certifikatuppdateringar när dina Adobe-utfärdade certifikat upphör att gälla
title: Hantera certifikatuppdateringar när dina Adobe-utfärdade certifikat upphör att gälla
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Hantera certifikatuppdateringar när dina Adobe-utfärdade certifikat går ut {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Det kan finnas tillfällen när du måste skaffa ett nytt certifikat från Adobe. När ett produktionscertifikat upphör att gälla upphör till exempel ett utvärderingscertifikat att gälla eller när du växlar från en utvärdering till ett produktionscertifikat. När ett certifikat upphör att gälla och du inte vill paketera om innehållet som använde det gamla certifikatet. Du kan göra licensservern uppmärksam på både gamla och nya certifikat.

Använd följande procedur för att uppdatera servern med de nya certifikaten:

1. (Valfritt) När du lägger till nya poster i en befintlig principuppdateringslista eller återkallningslista måste du se till att signera med de nya autentiseringsuppgifterna och använda det gamla certifikatet för att validera signaturen i den befintliga filen.

   Använd till exempel följande kommandorad för att lägga till en post i en befintlig principuppdateringslista som signerades med en annan autentiseringsuppgift:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Använd Java API för att uppdatera licensservern med den nya listan för principuppdatering eller återkallningslistan:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   eller:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   I referensimplementeringen är de egenskaper som du använder `HandlerConfiguration.RevocationList` och `HandlerConfiguration.PolicyUpdateList`. Uppdatera även certifikatet som används för att verifiera signaturerna: `RevocationList.verifySignature.X509Certificate`.

1. För att kunna förbruka innehåll som paketerats med de gamla certifikaten måste licensservern ha den gamla och nya inloggningsuppgifterna för licensservern och transportuppgifterna. Uppdatera licensservern med nya och gamla certifikat.

   För autentiseringsuppgifter för licensservern:

   * Kontrollera att den aktuella autentiseringsuppgiften skickas till konstruktorn `LicenseHandler`:

      * I referensimplementeringen anger du den via egenskapen `LicenseHandler.ServerCredential`.
      * I Adobe Access Server för skyddad direktuppspelning måste den aktuella autentiseringsuppgiften vara den första autentiseringsuppgiften som anges i `LicenseServerCredential`-elementet i filen flashaccess-tenant.xml.
   * Kontrollera att aktuella och gamla autentiseringsuppgifter anges till `AsymmetricKeyRetrieval`

      * I referensimplementeringen anger du den via egenskaperna `LicenseHandler.ServerCredential` och `AsymmetricKeyRetrieval.ServerCredential. n`.
      * I Adobe Access Server för skyddad direktuppspelning anges de gamla autentiseringsuppgifterna efter den första autentiseringsuppgiften i `LicenseServerCredential`-elementet i filen flashaccess-tenant.xml.

   För transportinloggningsuppgifterna:

   * Kontrollera att de aktuella autentiseringsuppgifterna skickas till metoden `HandlerConfiguration.setServerTransportCredential()`:

      * I referensimplementeringen anger du den via egenskapen `HandlerConfiguration.ServerTransportCredential`.
      * I Adobe Access Server för skyddad direktuppspelning måste den aktuella autentiseringsuppgiften vara den första autentiseringsuppgiften som anges i `TransportCredential`-elementet i filen flashaccess-tenant.xml.
   * Kontrollera att de gamla autentiseringsuppgifterna har angetts för `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * I referensimplementeringen anger du den via egenskaperna `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * I Adobe Access Server för skyddad direktuppspelning anges detta efter den första autentiseringen i `TransportCredential`-elementet i filen flashaccess-tenant.xml.




1. Uppdatera paketeringsverktygen för att säkerställa att de paketerar innehåll med de aktuella inloggningsuppgifterna. Kontrollera att det senaste licensservercertifikatet, transportcertifikatet och paketerarens autentiseringsuppgifter används för paketering.
1. Så här uppdaterar du nyckelserverns licensservercertifikat:

   * Uppdatera autentiseringsuppgifterna i klientserverns konfigurationsfil för Adobe Access Key Server. Inkludera både den gamla och nya Key Server-inloggningsuppgifterna i flashaccess-keyserver-tenant.xml.
   * Kontrollera att det aktuella certifikatet skickas till metoden `HandlerConfiguration.setKeyServerCertificate()`.

      * I referensimplementeringen anger du den via egenskapen `HandlerConfiguration.KeyServerCertificate`.
      * I Adobe Access Server för skyddad direktuppspelning anger du nyckelserverns certifikat i genom elementet Configuration/Tenant/Certificates/KeyServer.

