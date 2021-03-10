---
description: Om du vill spela upp DASH-innehåll som är ett resultat av innehållspaketering måste TVSDK-klienten hämta den innehållsdekrypteringsnyckel som skickades under paketeringsprocessen i arbetsflödet för hämtning av nycklar. Nyckeln för dekryptering av klientinnehåll levereras vanligtvis till klienten via en Widewin/PlayReady-licensserver som svar på ett eller flera HTTP/HTTPS-inlägg från klienten.
title: Översikt över arbetsflödet Klientnyckelbegäran
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Arbetsflöde för klientnyckelbegäran {#client-key-request-workflow-overview}

Om du vill spela upp DASH-innehåll som är ett resultat av innehållspaketering måste TVSDK-klienten hämta den innehållsdekrypteringsnyckel som skickades under paketeringsprocessen i arbetsflödet för hämtning av nycklar. Nyckeln för dekryptering av klientinnehåll levereras vanligtvis till klienten via en Widewin/PlayReady-licensserver som svar på ett eller flera HTTP/HTTPS-inlägg från klienten.

PSDK-klienten måste göra följande för att hämta innehållsdekrypteringsnyckeln:

* Hämta in innehållet i dess ssh box, ge det till plattformen och få som svar på en viktig begäran.
* Skicka nyckelbegäran till rätt Widewin/PlayReady-licensserver via en HTTP-POST.
* Skicka serverns svar till plattformen som extraherar klientens dekrypteringsnyckel från svaret och använder den för dekryptering av innehåll.

Om du vill skicka ut HTTP-POSTEN för nyckelbegäran måste din kod skicka licensserverns URL till PSDK-klienten tillsammans med eventuella extra data som måste bifogas till posten. Vilken URL och vilka data som ska skickas beror på vilken Widewin/PlayReady-tjänstleverantör du arbetar med. Om du t.ex. använder ExpressPlay för att tillhandahålla tjänsten skickar du rätt ExpressPlay-webbadress för licensserver/PlayReady-webbadress och bifogar den ExpressPlay-token som är associerad med innehållets krypteringsnyckel till den utgående nyckeln. Du kan hämta rätt ExpressPlay-webbadress för licensserver/PlayReady från ExpressPlay-dokumentationen.