---
seo-title: Skapa certifikatutfärdarens lista över enskilda användare
title: Skapa certifikatutfärdarens lista över enskilda användare
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Skapa certifikatutfärdarens lista över enskilda användare{#create-individualization-ca-crl}

Distributionsplatsen för listan över återkallade certifikat (CRL) ingår i varje datorcertifikat som utfärdas av individualiseringsservern. Under maskincertifikatverifieringen på licensservern hämtas denna CRL från den distributionsplats som anges i certifikatet (eller läses från cachen om den redan har hämtats) och kontrolleras för att säkerställa att certifikatet inte har återkallats.

>[!NOTE]
>
>Om du vill ange URL:en för CRL-distributionsplatsen måste du ange [!DNL AdobeInitial.properties] `cert.machine.crldp` fältet. Distributionspunkten kontrolleras *inte* av Primetime DRM för giltighet. Du måste verifiera att URL:en är giltig. Fel som uppstår till följd av en ogiltig URL visas inte förrän valideringsfel visas från licensservern.

Nedan finns enkla exempelinstruktioner för hur du använder OpenSSL för att skapa listor över återkallade certifikat som din licensserver kan använda. Adobe rekommenderar att du utför dessa steg på ett säkert sätt och i en säker miljö när en autentiseringsuppgift för Production Individualization CA har erhållits.

1. Ändra arbetskatalogen till den [!DNL create_crl] katalog som ingår i distributionen.
1. Kopiera din personliga certifikatutfärdare [!DNL pfx] till samma [!DNL create_crl] katalog.

   I följande steg antas att namnet på certifikatutfärdaren för Individualisering anges [!DNL i15n.pfx]. Justera efter behov.
1. Extrahera Individualization CA- [!DNL pfx] filens privata nyckel.

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

   I det här exemplet skapas en CRL med en standardgiltighetsperiod på en månad. Använd alternativen `-crldays` och `-crlhours` för att åsidosätta standardvärdena.

   När du skapar en CRL används den [!DNL index] och den [!DNL crlnumber] fil som du har i [!DNL openssl.conf]. Som standard används [!DNL demoCA] platsen i arbetskatalogen. Exempel [!DNL index] och [!DNL crlnumber] filer inkluderas i angiven [!DNL demoCA] katalog.

1. Distribuera CRL-filen som genererades i föregående steg till en lämplig plats som licensservern kan nå (till exempel: personaliseringsserver [!DNL ROOT]).
1. Starta om licensservern när listan över återkallade certifikat är på plats.
