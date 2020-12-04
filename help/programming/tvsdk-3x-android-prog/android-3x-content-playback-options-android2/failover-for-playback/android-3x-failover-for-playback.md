---
description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.
seo-description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.
seo-title: Uppspelning och failover
title: Uppspelning och failover
uuid: 511f16b9-2b86-42c1-8d89-09b26534200b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Översikt {#playback-and-failover-overview}

Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.

>[!IMPORTANT]
>
>Primetime kan inte skydda sig mot fel, t.ex. ett avbrott i en Internet-leverantör eller en kabelbortkoppling.

Primetime-direktuppspelning ger failover-skydd för att skydda uppspelningen från vissa fjärrserverfel eller driftfel, vilket ger en bättre tittarupplevelse. Trots överföringsproblem implementerar TVSDK redundansskydd för att minimera uppspelningsavbrott och få en sömlös uppspelning. Videospelaren växlar automatiskt till en uppsättning säkerhetskopieringsmedia när hela återgivningar eller fragment inte är tillgängliga.