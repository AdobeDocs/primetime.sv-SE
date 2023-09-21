---
title: Använda skyddsprofiler för utdata
description: Använda skyddsprofiler för utdata
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Använda skyddsprofiler för utdata{#using-output-protection-policies}

**Skyddspolicyer för vinstdrivande produktioner**

Widewin stöder både analoga och digitala begränsningar för skydd av utdata. Läs dokumentationen från din Widewin-leverantör om hur du bifogar dessa policyer till genererade licenser.

Om du använder Expresplay som Widewin-tjänstleverantör kopplar du principer för digitalt utdataskydd vid tokengenereringstid via hdcpOutputControl-flaggan: Tillåtna värden är 0, 1, 2 där 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Både HDCP_V1 och HDCP_V2 tillämpar HDCP version 1.X respektive 2.X.

Uttrycket har för närvarande inte stöd för att koppla analoga utdatabegränsningar

**Principer för PlayReady-utdataskydd**

PlayReady har också inbyggt stöd för både analoga och digitala utdataskyddsbegränsningar. De värden för skyddsnivå för utdata som du kan ange. Sidan [Utdataskyddsnivåer](https://msdn.microsoft.com/en-us/library/dn468831.aspx) dokumenterar de värden som du kan ange och deras förväntade klientbeteende.

Om du använder Expresplay ska du bifoga värden för skyddsnivå vid generering av token via compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL och unknownOutputBehavior-flaggan. Dessa dokumenteras på [Begäran om PlayReady-licenstoken](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
