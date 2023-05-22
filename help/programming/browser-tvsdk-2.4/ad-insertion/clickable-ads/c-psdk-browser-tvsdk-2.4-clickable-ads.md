---
description: Browser TVSDK förser din videoapp med den information som behövs för att svara på en klickbar annons.
title: Klickbara annonser
exl-id: 5fd8b38d-bde7-4d80-bfb0-3390c8f2665c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Översikt {#clickable-ads-overview}

Browser TVSDK förser din videoapp med den information som behövs för att svara på en klickbar annons.

När en användare klickar på en klickbar annons är ett typiskt svar från en videoapp att öppna ett nytt webbläsarfönster och navigera till den URL som är associerad med annonsen. För att underlätta detta skickar webbläsaren TVSDK meddelanden om att appen kan använda för att hantera klickningsprocessen.

I appen kan du ge användaren en kontroll att klicka (t.ex. en knapp) medan den klickbara annonsen spelas upp. Du måste skapa hanterare för händelser som utlöses av Browser TVSDK och som är kopplade till annonsen (t.ex. start, annons, klickad och slutförd). Slutligen måste du implementera de specifika beteenden som appen följer efter en användares annonsklickning (t.ex. om annonsen ska pausas, om klicknings-URL:en ska visas och så vidare).

>[!NOTE]
>
>Referensspelaren som ingår i Browser TVSDK innehåller en möjlig arbetslösning för bearbetning av klickbara annonser.
