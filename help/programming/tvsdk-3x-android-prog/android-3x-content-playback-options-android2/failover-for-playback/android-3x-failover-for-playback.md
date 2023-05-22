---
description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.
title: Uppspelning och failover
exl-id: ba8326ba-4ff1-46ad-bd18-9c83147ab619
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Översikt {#playback-and-failover-overview}

Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade media.

>[!IMPORTANT]
>
>Primetime kan inte skydda sig mot fel, t.ex. ett avbrott i en Internet-leverantör eller en kabelbortkoppling.

Primetime-direktuppspelning ger failover-skydd för att skydda uppspelningen från vissa fjärrserverfel eller driftfel, vilket ger en bättre tittarupplevelse. Trots överföringsproblem implementerar TVSDK redundansskydd för att minimera uppspelningsavbrott och få en sömlös uppspelning. Videospelaren växlar automatiskt till en uppsättning säkerhetskopieringsmedia när hela återgivningar eller fragment inte är tillgängliga.
