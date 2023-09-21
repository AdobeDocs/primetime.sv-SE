---
description: Browser TVSDK förser din videoapp med den information som behövs för att svara på en klickbar annons.
title: Klickbara annonser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Ökning {#clickable-ads-overview}

Browser TVSDK förser din videoapp med den information som behövs för att svara på en klickbar annons.

När en användare klickar på en klickbar annons är ett typiskt svar från en videoapp att öppna ett nytt webbläsarfönster och navigera till den URL som är associerad med annonsen. För att underlätta detta skickar webbläsaren TVSDK meddelanden om att appen kan använda för att hantera klickningsprocessen.

I appen kan du ge användaren en kontroll att klicka (t.ex. en knapp) medan den klickbara annonsen spelas upp. Du måste skapa hanterare för händelser som utlöses av Browser TVSDK och som är kopplade till annonsen (t.ex. start, annons, klickad och slutförd). Slutligen måste du implementera de specifika beteenden som appen följer efter en användares annonsklickning (t.ex. om annonsen ska pausas, om klicknings-URL:en ska visas och så vidare).

>[!NOTE]
>
>Referensspelaren som ingår i Browser TVSDK innehåller en möjlig arbetslösning för bearbetning av klickbara annonser.
