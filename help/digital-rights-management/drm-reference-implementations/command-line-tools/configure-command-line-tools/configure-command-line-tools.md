---
title: Konfigurera och köra kommandoradsverktygen
description: Konfigurera och köra kommandoradsverktygen
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
