---
description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade medier.
title: Uppspelning och failover
exl-id: 45693d0b-a5fb-4716-a410-ac323950f40b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Översikt {#playback-and-failover-overview}

Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade medier.

Primetime kan inte skydda mot fel som ett avbrott i en Internet-leverantör eller en kabelbortkoppling. Primetime-strömning ger dock failover-skydd för att skydda uppspelningen från vissa fjärrserverfel eller driftfel, vilket ger en bättre upplevelse för tittarna. TVSDK implementerar redundansskydd för att minimera uppspelningsavbrott och få en sömlös uppspelning trots överföringsproblem. Videospelaren växlar automatiskt till en uppsättning säkerhetskopieringsmedia när hela återgivningar eller fragment inte är tillgängliga.
