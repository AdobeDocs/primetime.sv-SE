---
title: Skapa certifikatutfärdarens lista över enskilda användare
description: Skapa certifikatutfärdarens lista över enskilda användare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Skapa certifikatutfärdarens lista över enskilda användare{#create-individualization-ca-crl}

Distributionsplatsen för listan över återkallade certifikat (CRL) ingår i varje datorcertifikat som utfärdas av individualiseringsservern. Under maskincertifikatverifieringen på licensservern hämtas denna CRL från den distributionsplats som anges i certifikatet (eller läses från cachen om den redan har hämtats) och kontrolleras för att säkerställa att certifikatet inte har återkallats.

>[!NOTE]
>
>Om du vill ange URL:en för CRL-distributionsplatsen måste du ange [!DNL AdobeInitial.properties] `cert.machine.crldp` fält. Den här distributionsplatsen är *not* kontrolleras av Primetime DRM för giltighet. Du måste verifiera att URL:en är giltig. Fel som uppstår till följd av en ogiltig URL visas inte förrän valideringsfel visas från licensservern.

Nedan finns enkla exempelinstruktioner för hur du använder OpenSSL för att skapa listor över återkallade certifikat som din licensserver kan använda. Adobe rekommenderar att du utför dessa steg på ett säkert sätt och i en säker miljö när en autentiseringsuppgift för Production Individualization CA har erhållits.

1. Ändra arbetskatalogen till [!DNL create_crl] katalog som ingår i den här distributionen.
1. Kopiera din personliga certifikatutfärdare [!DNL pfx] till samma [!DNL create_crl] katalog.

   I följande steg antas att namnet på certifikatutfärdarens pfx för Individualisering anges [!DNL i15n.pfx]. Justera efter behov.
1. Extrahera den enskilda certifikatutfärdaren [!DNL pfx] filens privata nyckel.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Konvertera den privata nyckeln till [!DNL pksc8] format.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Generera CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   I det här exemplet skapas en CRL med en standardgiltighetsperiod på en månad. Använd `-crldays` och `-crlhours` alternativ för att åsidosätta standardvärdena.

   När en lista över återkallade certifikat skapas används [!DNL index] och [!DNL crlnumber] i [!DNL openssl.conf]. Som standard är [!DNL demoCA] plats i arbetskatalogen används. Exempel [!DNL index] och [!DNL crlnumber] -filerna ingår i [!DNL demoCA] katalog.

1. Distribuera CRL-filen som genererades i föregående steg till en lämplig plats som kan nås av licensservern (till exempel en individualiseringsserver) [!DNL ROOT]).
1. Starta om licensservern när listan över återkallade certifikat är på plats.
