---
seo-title: Konfigurera och köra kommandoradsverktygen
title: Konfigurera och köra kommandoradsverktygen
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Konfigurera och köra kommandoradsverktygen {#configure-and-run-the-command-line-tools}

Kommandoradsverktygen har associerade egenskaper som du måste ange värden för [!DNL flashaccesstools.properties] innan ** du kör verktygen. I vissa kommandoradsverktyg kan du även ange egenskapsvärden från kommandoraden. Värden som du anger från kommandoraden har företräde framför värden som du anger från [!DNL flashaccesstools.properties].

Du måste ändra inställningarna i följande avsnitt i för [!DNL flashaccesstools.properties] att aktivera motsvarande kommandoradsverktyg som du tänker använda:

* **Egenskaper** för Media Packager - (för [!DNL AdobePackager.jar])

* **Egenskaper** för Listhanteraren för principuppdatering och Hanteraren för återkallningslistor - (för [!DNL AdobePolicyUpdateListManager.jar] och [!DNL AdobeRevocationListManager.jar])

* **Policyhanterarens egenskaper** - (för [!DNL AdobePolicyManager.jar])

* **Egenskaper** för licensgenerator - (för [!DNL AdobeLicenseGenerator.jar])