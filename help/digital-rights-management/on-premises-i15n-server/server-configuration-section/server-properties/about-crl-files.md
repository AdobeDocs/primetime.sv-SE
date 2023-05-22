---
title: Om CRL-filer
description: Om CRL-filer
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

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

Om du vill veta mer om vilka externa CRL:er som kan användas av licensservrarna kontaktar du Adobe Support.

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

Utöver de externt värdbaserade CRL:erna kan du skapa och underhålla ytterligare en CRL. Det här är Individualization CA CRL, enligt specifikationen i [Skapa certifikatutfärdarens lista över enskilda användare](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) i det här dokumentet.

CRL:er är schemalagda att uppdateras 45 dagar innan de upphör att gälla. På så sätt får du tillräckligt med tid för att hämta och installera nyligen genererade listor över återkallade certifikat från Internet. Du måste uppdatera CRL-filer innan de går ut.
