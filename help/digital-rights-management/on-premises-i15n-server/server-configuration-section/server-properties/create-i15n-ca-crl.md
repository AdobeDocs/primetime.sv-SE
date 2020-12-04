---
seo-title: Skapa certifikatutfärdarens lista över enskilda användare
title: Skapa certifikatutfärdarens lista över enskilda användare
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Skapa certifikatutfärdarens CRL{#create-individualization-ca-crl}

Distributionsplatsen för listan över återkallade certifikat (CRL) ingår i varje datorcertifikat som utfärdas av individualiseringsservern. Under maskincertifikatverifieringen på licensservern hämtas denna CRL från den distributionsplats som anges i certifikatet (eller läses från cachen om den redan har hämtats) och kontrolleras för att säkerställa att certifikatet inte har återkallats.

>[!NOTE]
>
>Om du vill ange URL:en för CRL-distributionsplatsen måste du ange fältet [!DNL AdobeInitial.properties] `cert.machine.crldp`. Distributionspunkten är *inte* kontrollerad av Primetime DRM för giltighet. Du måste verifiera att URL:en är giltig. Fel som uppstår till följd av en ogiltig URL visas inte förrän valideringsfel visas från licensservern.

Nedan finns enkla exempelinstruktioner för hur du använder OpenSSL för att skapa listor över återkallade certifikat som din licensserver kan använda. Adobe rekommenderar att du utför dessa steg på ett säkert sätt och i en säker miljö när en autentiseringsuppgift för Production Individualization CA har erhållits.

1. Ändra arbetskatalogen till katalogen [!DNL create_crl] som ingår i den här distributionen.
1. Kopiera din enskilda CA [!DNL pfx] till samma [!DNL create_crl]-katalog.

   I följande steg antas att namnet på den enskilda certifikatutfärdarens pfx är [!DNL i15n.pfx]. Justera efter behov.
1. Extrahera Individualization CA [!DNL pfx]-filens privata nyckel.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Konvertera den privata nyckeln till formatet [!DNL pksc8].

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Generera CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   I det här exemplet skapas en CRL med en standardgiltighetsperiod på en månad. Använd alternativen `-crldays` och `-crlhours` för att åsidosätta standardvärdena.

   När du skapar en CRL används den [!DNL index]- och [!DNL crlnumber]-fil som du refererar till i din [!DNL openssl.conf]. Som standard används platsen [!DNL demoCA] i arbetskatalogen. Exempel på [!DNL index]- och [!DNL crlnumber]-filer finns i den angivna [!DNL demoCA]-katalogen.

1. Distribuera CRL-filen som genererades i föregående steg till en lämplig plats som licensservern kan nå (till exempel: individualiseringsserver [!DNL ROOT]).
1. Starta om licensservern när listan över återkallade certifikat är på plats.
