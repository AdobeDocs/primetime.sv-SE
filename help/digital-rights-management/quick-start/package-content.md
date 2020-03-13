---
seo-title: Paketera krypterat innehåll
title: Paketera krypterat innehåll
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Paketera krypterat innehåll{#package-encrypted-content}

1. Kopiera `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` katalogen till det lokala filsystemet.
1. I den lokala `Command Line Tools\` mappen uppdaterar du `flashaccesstools.properties` filen så att den fungerar med servern.

   Du måste ändra minst följande egenskaper:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: Sökvägen till ditt licensservercertifikat (det slutar vanligtvis med [!DNL .cer], [!DNL .der] eller [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: Licensserverns URL, t.ex.:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: Sökvägen till ditt transportcertifikat (det avslutas vanligtvis med [!DNL .cer], [!DNL .der]eller [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: Sökvägen till ditt Packager-certifikat (detta slutar med [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: Lösenordet för ditt Packager-certifikat.
   >[!NOTE]
   >
   >Kontrollera att du inte ändrar lösenordet.

1. Skapa en profil.

   Kör följande kommando i den lokala `Command Line Tools\` mappen:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Det här kommandot skapar en principfil med namnet [!DNL examplepolicy.pol] som använder anonym serverautentisering ( `-x` alternativet).
1. Kopiera MP4-, FLV- eller F4V-videofilen som du vill kryptera till den lokala `Command Line Tools\` mappen.
1. Paketera innehållet.

   Låt oss säga att källvideofilen är [!DNL sample.mp4]. Kör följande kommando i den lokala `Command Line Tools\` mappen:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Om du vill paketera HLS-, HDS- eller DASH-innehåll måste du använda ett annat paketeringsverktyg, till exempel [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Kopiera de krypterade filartefakterna (i det här fallet [!DNL sample_encrypted.mp4] och [!DNL sample_encrypted.mp4.metadata]) till `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

Nu har du slutfört paketeringsfasen av processen.

>[!NOTE]
>
>Mer information om kommandoradsverktyg för att paketera innehåll, skapa principer och mycket mer finns i [Adobe Primetimes DRM-kommandoradsverktyg](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
