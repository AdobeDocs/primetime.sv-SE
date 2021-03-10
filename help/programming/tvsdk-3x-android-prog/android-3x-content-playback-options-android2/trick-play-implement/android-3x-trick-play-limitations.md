---
title: Begränsningar och beteenden för trick play
description: Begränsningar och beteenden för trick play
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Begränsningar och beteenden för trick play {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Begränsningar för uppspelningsläge för trick:

* Den överordnad spelningslistan måste innehålla segment som bara är för Iframe.

   Endast nyckelbildrutorna från Iframe-spåret visas på skärmen.
* Ljudspåret och undertexter är inaktiverade.
* Uppspelning och paus är aktiverat.
* Du kan avsluta trippelläget i valfri tillåten uppspelningshastighet (uppspelning eller paus).
* När annonser har infogats i strömmen:

   * Du kan bara lura att spela medan du spelar huvudinnehållet. Ett fel skickas om du försöker byta för att lura till dig att spela under en annonsbrytning.
   * Efter att tricket har spelats upp ignoreras annonsbrytningar och inga annonshändelser utlöses.
   * Tidslinjen som TVSDK visar spelaren ändras inte även om annonsbrytningar hoppas över.
   * Det aktuella tidsvärdet hoppar framåt (snabbt framåt) eller bakåt (vid snabb tillbakaspolning) med varaktigheten för den överhoppade annonsbrytningen.

      Detta hoppbeteende för den aktuella tiden gör att strömmens varaktighet förblir oförändrad under trippelning. Spelaren kan bara spåra tiden i förhållande till huvudinnehållet. Inga tidshopp utförs för de värden som returneras för lokal tid när en annons hoppas över.
   * `MediaPlayerEvent.AD_BREAK_SKIPPED`-händelsen skickas omedelbart innan en annonsbrytning håller på att hoppas över.

      Spelaren kan använda den här händelsen för att implementera anpassad logik som är relaterad till de överhoppade annonsbrytningarna.

   * När du avslutar trick play anropas samma annonsuppspelningsprincip som när sökningen avslutas.

      Precis som vid sökning beror beteendet på om programmets uppspelningsprincip skiljer sig från standardinställningen. Standardinställningen är att den senast hoppade annonsbrytningen spelas upp där du kommer ut ur tricksspelet.