---
seo-title: Konfigurera och köra kommandoradsverktygen
title: Konfigurera och köra kommandoradsverktygen
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Konfigurera och kör kommandoradsverktygen {#configure-and-run-the-command-line-tools}

Kommandoradsverktygen har associerade egenskaper som du måste ange värden för i [!DNL flashaccesstools.properties] *innan du kör verktygen.* I vissa kommandoradsverktyg kan du även ange egenskapsvärden från kommandoraden. Värden som du anger från kommandoraden åsidosätter värden som du anger från [!DNL flashaccesstools.properties].

Du måste ändra inställningarna i följande avsnitt av [!DNL flashaccesstools.properties] för att aktivera motsvarande kommandoradsverktyg som du tänker använda:

* **Egenskaper**  för Media Packager - (för  [!DNL AdobePackager.jar])

* **Egenskaper**  för listhanteraren för principuppdatering och listhanteraren för återkallning (för  [!DNL AdobePolicyUpdateListManager.jar] och  [!DNL AdobeRevocationListManager.jar])

* **Policy Manager-egenskaper** - (för  [!DNL AdobePolicyManager.jar])

* **Egenskaper**  för licensgenerator - (för  [!DNL AdobeLicenseGenerator.jar])