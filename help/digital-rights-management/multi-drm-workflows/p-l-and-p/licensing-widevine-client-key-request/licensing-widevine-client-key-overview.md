---
description: Om du vill spela upp DASH-innehåll som är ett resultat av innehållspaketering måste TVSDK-klienten hämta den innehållsdekrypteringsnyckel som skickades under paketeringsprocessen i arbetsflödet för hämtning av nycklar. Nyckeln för dekryptering av klientinnehåll levereras vanligtvis till klienten via en Widewin/PlayReady-licensserver som svar på ett eller flera HTTP/HTTPS-inlägg från klienten.
seo-description: Om du vill spela upp DASH-innehåll som är ett resultat av innehållspaketering måste TVSDK-klienten hämta den innehållsdekrypteringsnyckel som skickades under paketeringsprocessen i arbetsflödet för hämtning av nycklar. Nyckeln för dekryptering av klientinnehåll levereras vanligtvis till klienten via en Widewin/PlayReady-licensserver som svar på ett eller flera HTTP/HTTPS-inlägg från klienten.
seo-title: Översikt över arbetsflödet Klientnyckelbegäran
title: Översikt över arbetsflödet Klientnyckelbegäran
uuid: 2f01f0ae-adbf-42fa-a908-4b5b9410a26d
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Arbetsflöde för klientnyckelbegäran {#client-key-request-workflow-overview}

Om du vill spela upp DASH-innehåll som är ett resultat av innehållspaketering måste TVSDK-klienten hämta den innehållsdekrypteringsnyckel som skickades under paketeringsprocessen i arbetsflödet för hämtning av nycklar. Nyckeln för dekryptering av klientinnehåll levereras vanligtvis till klienten via en Widewin/PlayReady-licensserver som svar på ett eller flera HTTP/HTTPS-inlägg från klienten.

PSDK-klienten måste göra följande för att hämta innehållsdekrypteringsnyckeln:

* Hämta in innehållet i dess ssh box, ge det till plattformen och få som svar på en viktig begäran.
* Skicka nyckelbegäran till rätt Widewin/PlayReady-licensserver via HTTP POST.
* Skicka serverns svar till plattformen som extraherar klientens dekrypteringsnyckel från svaret och använder den för dekryptering av innehåll.

Om du vill skicka ut HTTP POST för nyckelbegäran måste din kod skicka licensserverns URL till PSDK-klienten tillsammans med eventuella extra data som måste bifogas till posten. Vilken URL och vilka data som ska skickas beror på vilken Widewin/PlayReady-tjänstleverantör du arbetar med. Om du t.ex. använder ExpressPlay för att tillhandahålla tjänsten skickar du rätt ExpressPlay-webbadress för licensserver/PlayReady-webbadress och bifogar den ExpressPlay-token som är associerad med innehållets krypteringsnyckel till den utgående nyckeln. Du kan hämta rätt ExpressPlay-webbadress för licensserver/PlayReady från ExpressPlay-dokumentationen.