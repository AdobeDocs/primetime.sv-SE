---
seo-title: Om CRL-filer
title: Om CRL-filer
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Om CRL-filer {#about-crl-files}

För att enskilda servrar och licensservrar ska fungera på rätt sätt måste flera CRL-filer (Certificate Revocation List) vara cachelagrade till disk på den programserver som körs (t.ex. Tomcat). Nya CRL-filer måste laddas ned och cachas på disk regelbundet. Om giltighetsperioden för CRL-filer på disken tillåts upphöra kommer Individualization Server att vägra att individualisera klienter och License Server kommer att vägra att utfärda licenser.

De listor över återkallade certifikat som cachas till disk måste ha filnamn som matchar motsvarande URL:er. Specialtecken som kolon &#39;:&#39; och &#39;/&#39; snedstreck konverteras till understreck &#39;_&#39; i filnamnen.

Nedan följer en lista över externa CRL:er som används av både Individualization- och License-servrar:

* **Mellanliggande CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * Fil: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Giltighet: Gäller i cirka 12 månader från det att fotot skapades

* **Root-CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * Fil: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Giltighet: Gäller i cirka 5 år från skapandet

* **Senaste CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * Fil: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Giltighet: Gäller i cirka 3 månader från det att fotot skapades

Följande är externt värdbaserade CRL:er som bara används av licensservrarna:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* Fil: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Giltighet: Gäller i cirka 3 månader från det att fotot skapades

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* Fil: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Giltighet: Gäller i cirka 3 månader från det att fotot skapades

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* Fil: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Giltighet: Gäller i cirka 3 månader från det att fotot skapades

Utöver de tidigare nämnda CRL:erna måste du skapa och underhålla ytterligare en CRL. Det här är CRL:en för enskilt certifikatutfärdare, enligt vad som anges i avsnittet [Skapa CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) för enskilt certifikatutfärdare i det här dokumentet.

CRL:er är schemalagda att uppdateras 45 dagar innan de upphör att gälla. På så sätt får du tillräckligt med tid för att hämta och installera nyligen genererade listor över återkallade certifikat från Internet. Du måste uppdatera CRL-filer innan de går ut.
