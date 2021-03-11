---
title: Konfigurera och köra kommandoradsverktygen
description: Konfigurera och köra kommandoradsverktygen
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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