---
description: SEES-referensservern visar hur du aktiverar den enhetsbindande tillståndstjänsten med ExpressPlay.
title: Enhetsbindningsbehörighet för referenstjänst
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Referenstjänst: Enhetsbindningsberättigande {#reference-service-device-binding-entitlement}

SEES-referensservern visar hur du aktiverar den enhetsbindande tillståndstjänsten med ExpressPlay.

>[!NOTE]
>
>Den enhetsbundna berättigandetjänsten kan också vara tidsbunden eller ge uthyrningstid.

Om du vill starta `device_id`-informationen ska du spela upp ett dummy M3U8-innehåll. Du kan sedan bädda in en cookie i ExpressPlay-token, generera en SPC (som innehåller `device_id`) och skicka en `getToken` till ExpressPlay-servern.

![](assets/fees-device-binding.png)

Sekvensen börjar med att spela upp en dummy M3U8. En cookie skickas till SEES-servern för att hämta ExpressPlay-token-URL:en. När du har tagit emot den cookie-bundna ExpressPlay-token-URL:en är nästa steg att generera SPC:n och skicka den till ExpressPlay-servern. ExpressPlay-servern extraherar `device_id` från SPC, cookien från ExpressPlay-token-URL:en och placerar cookien och `device_id` i transaktionsloggen.

Klienten gör en verklig licensbegäran till SEES som skickar samma cookie. SEES använder cookien för att hämta `device_id` från ExpressPlay-servern.

SEES begär en ExpressPlay-token som är enhetsbunden såväl som tidsbunden och returnerar denna token till klienten.

Klienten skickar licensbegäran med ExpressPlay-token.

ExpressPlay-servern jämför `device_id` i SPC med `device_id` i ExpressPlay-token. ExpressPlay-servern utfärdar bara en licens om de två `device_id`-värdena matchar.
