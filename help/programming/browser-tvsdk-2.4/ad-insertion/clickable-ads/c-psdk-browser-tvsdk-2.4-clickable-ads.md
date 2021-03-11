---
description: Browser TVSDK förser din videoapp med den information som behövs för att svara på en klickbar annons.
title: Klickbara annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Översikt {#clickable-ads-overview}

Browser TVSDK förser din videoapp med den information som behövs för att svara på en klickbar annons.

När en användare klickar på en klickbar annons är ett typiskt svar från en videoapp att öppna ett nytt webbläsarfönster och navigera till den URL som är associerad med annonsen. För att underlätta detta skickar webbläsaren TVSDK meddelanden om att din app kan använda för att hantera klickningsprocessen.

I appen kan du ge användaren en kontroll att klicka (t.ex. en knapp) medan den klickbara annonsen spelas upp. Du måste skapa hanterare för händelser som utlöses av Browser TVSDK och som är kopplade till annonsen (t.ex. start, annons, klickad och slutförd). Slutligen måste du implementera de specifika beteenden som appen följer efter en användares annonsklickning (t.ex. om annonsen ska pausas, om klicknings-URL:en ska visas och så vidare).

>[!NOTE]
>
>Referensspelaren som ingår i Browser TVSDK innehåller en möjlig arbetslösning för bearbetning av klickbara annonser.