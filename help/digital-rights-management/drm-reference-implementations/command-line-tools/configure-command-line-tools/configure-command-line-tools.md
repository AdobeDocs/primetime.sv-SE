---
title: Konfigurera och köra kommandoradsverktygen
description: Konfigurera och köra kommandoradsverktygen
copied-description: true
exl-id: ff0d4316-24e6-4a34-b332-abd737d6fcf9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Konfigurera och köra kommandoradsverktygen {#configure-and-run-the-command-line-tools}

Kommandoradsverktygen har associerade egenskaper som du måste ange värden för i [!DNL flashaccesstools.properties] *före* du kör verktygen. I vissa kommandoradsverktyg kan du även ange egenskapsvärden från kommandoraden. Värden som du anger från kommandoraden åsidosätter värden som du anger från [!DNL flashaccesstools.properties].

Du måste ändra inställningarna i följande avsnitt i [!DNL flashaccesstools.properties] för att aktivera motsvarande kommandoradsverktyg som du tänker använda:

* **Egenskaper för Media Packager** - (för [!DNL AdobePackager.jar])

* **Egenskaper för listhanteraren för principuppdatering och återkallningslisthanteraren** - (för [!DNL AdobePolicyUpdateListManager.jar] och [!DNL AdobeRevocationListManager.jar])

* **Egenskaper för principhanteraren** - (för [!DNL AdobePolicyManager.jar])

* **Egenskaper för licensgenerator** - (för [!DNL AdobeLicenseGenerator.jar])
