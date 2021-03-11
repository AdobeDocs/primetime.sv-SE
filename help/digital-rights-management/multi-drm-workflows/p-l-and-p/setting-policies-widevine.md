---
title: Använda skyddsprofiler för utdata
description: Använda skyddsprofiler för utdata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Använda utdataskyddsprofiler{#using-output-protection-policies}

**Skyddspolicyer för vinstdrivande produktioner**

Widewin stöder både analoga och digitala begränsningar för skydd av utdata. Läs dokumentationen från din Widewin-leverantör om hur du bifogar dessa policyer till genererade licenser.

Om du använder Expresshow som Widewin-tjänsteleverantör måste du bifoga principer för skydd av digitala utdata vid tokengenerering via hdcpOutputControl-flaggan:
Tillåtna värden är 0, 1, 2 där 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Både HDCP_V1 och HDCP_V2 tillämpar HDCP version 1.X respektive 2.X.

Uttrycket stöder för närvarande inte koppling av analoga utdatabegränsningar

**Principer för PlayReady-utdataskydd**

PlayReady har också inbyggt stöd för både analoga och digitala utdataskyddsbegränsningar. De värden för skyddsnivå för utdata som du kan ange. På sidan [Utdataskyddsnivåer](https://msdn.microsoft.com/en-us/library/dn468831.aspx) dokumenteras de värden som du kan ange och deras förväntade klientbeteende.

Om du använder Expresplay ska du bifoga värden för skyddsnivå vid generering av token via compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL och unknownOutputBehavior-flaggan. Dessa beskrivs i [PlayReady License Token Request](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
