---
description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.
title: Uppspelning och failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Ökning {#playback-and-failover-overview}

Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.

>[!IMPORTANT]
>
>Primetime kan inte skydda sig mot fel, t.ex. ett avbrott i en Internet-leverantör eller en kabelbortkoppling.

Primetime-direktuppspelning ger failover-skydd för att skydda uppspelningen från vissa fjärrserverfel eller driftfel, vilket ger en bättre tittarupplevelse. Trots överföringsproblem implementerar TVSDK redundansskydd för att minimera uppspelningsavbrott och få en sömlös uppspelning. Videospelaren växlar automatiskt till en uppsättning säkerhetskopieringsmedia när hela återgivningar eller fragment inte är tillgängliga.
