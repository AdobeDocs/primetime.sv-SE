---
seo-title: Använda skyddsprofiler för utdata
title: Använda skyddsprofiler för utdata
uuid: f00d2a97-0036-41a6-ab44-391cc40b146e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Använda skyddsprofiler för utdata{#using-output-protection-policies}

**Skyddspolicyer för vinstdrivande produktioner**

Widewin stöder både analoga och digitala begränsningar för skydd av utdata. Läs dokumentationen från din Widewin-leverantör om hur du bifogar dessa policyer till genererade licenser.

Om du använder Expresshow som Widewin-tjänsteleverantör måste du bifoga principer för skydd av digitala utdata vid tokengenerering via hdcpOutputControl-flaggan:
Tillåtna värden är 0, 1, 2 där 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Både HDCP_V1 och HDCP_V2 tillämpar HDCP version 1.X respektive 2.X.

Uttrycket stöder för närvarande inte koppling av analoga utdatabegränsningar

**Principer för PlayReady-utdataskydd**

PlayReady har också inbyggt stöd för både analoga och digitala utdataskyddsbegränsningar. De värden för skyddsnivå för utdata som du kan ange. På sidan [Utdataskyddsnivåer](https://msdn.microsoft.com/en-us/library/dn468831.aspx) dokumenteras de värden som du kan ange och deras förväntade klientbeteende.

Om du använder Expresplay ska du bifoga värden för skyddsnivå vid generering av token via compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL och unknownOutputBehavior-flaggan. Dessa beskrivs på [PlayReady-licenstokenbegäran](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
