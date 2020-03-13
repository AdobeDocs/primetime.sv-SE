---
description: Det finns vissa begränsningar och vissa problem i hur trickläget fungerar.
seo-description: Det finns vissa begränsningar och vissa problem i hur trickläget fungerar.
seo-title: Begränsningar och beteenden för trick play
title: Begränsningar och beteenden för trick play
uuid: 0e84c9ef-fc18-4667-ad17-7f4777b552ba
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Begränsningar och beteenden för trick play{#limitations-and-behavior-for-trick-play}

Det finns vissa begränsningar och vissa problem i hur trickläget fungerar.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Här är begränsningarna för trickläge:

* Huvudspelningslistan måste innehålla segment med bara I-frame. Endast nyckelbildrutorna från I-frame-spåret visas på skärmen.
* Ljudspåret och undertexter är inaktiverade.
* Logiken för anpassad bithastighet (ABR) är inaktiverad. TVSDK väljer en bithastighet mellan den lägsta angivna hastigheten och 800 kbit/s och använder den hastigheten under hela uppspelningssessionen.
* Uppspelning och paus är aktiverat.
* Sökning tillåts inte. Om du vill söka anropar du `pause` för att avsluta trickläget och sedan anropa `seek`.

* Du kan gå från trippelläge till tillåten uppspelningshastighet (uppspelning eller paus).
* När annonser har infogats i strömmen:

   * Du kan bara lura att spela medan du spelar huvudinnehållet. Ett fel skickas om du försöker byta för att lura till dig att spela under en annonsbrytning.
   * Efter att tricket har spelats upp ignoreras annonsbrytningar och inga annonshändelser utlöses.
   * Tidslinjen som visas av TVSDK för spelarprogrammet ändras inte även om annonsbrytningar hoppas över.
   * Det aktuella tidsvärdet hoppar framåt (snabbt framåt) eller bakåt (vid snabb tillbakaspolning) med varaktigheten för den överhoppade annonsbrytningen. Detta hoppbeteende för den aktuella tiden gör att strömmens varaktighet förblir oförändrad under trippelning. Spelarprogrammet kan hämta det lokala tidsvärdet för att spåra tiden i förhållande enbart till huvudinnehållet. Inga tidshopp utförs för de värden som returneras för lokal tid när en annons hoppas över.
   * Händelsen `MediaPlayerEvent.AD_BREAK_SKIPPED` skickas omedelbart innan en annonsbrytning håller på att hoppas över. Spelaren kan använda den här händelsen för att implementera anpassad logik som är relaterad till de överhoppade annonsbrytningarna.
   * När du avslutar trick play anropas samma annonsuppspelningsprincip som när sökningen avslutas.

      Som vid sökning beror därför beteendet på om programmets uppspelningsprincip skiljer sig från standardinställningen. Som standard spelas den senast hoppade annonsbrytningen upp där du kommer ur trickläget.

