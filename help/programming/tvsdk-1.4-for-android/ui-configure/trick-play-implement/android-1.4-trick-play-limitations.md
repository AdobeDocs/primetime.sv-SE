---
description: Det finns vissa begränsningar och vissa problem i hur trickläget fungerar.
title: Begränsningar och beteenden för trick play
exl-id: 98558970-9e5e-4dc1-a327-63d9db1d4fed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Begränsningar och beteenden för trick play{#limitations-and-behavior-for-trick-play}

Det finns vissa begränsningar och vissa problem i hur trickläget fungerar.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Här är begränsningarna för trickläge:

* Den överordnad spellistan måste innehålla segment som bara är för bildrutor. Endast nyckelbildrutorna från I-frame-spåret visas på skärmen.
* Ljudspåret och undertexter är inaktiverade.
* Logiken för anpassad bithastighet (ABR) är inaktiverad. TVSDK väljer en bithastighet mellan den lägsta angivna hastigheten och 800 kbit/s och använder den hastigheten under hela uppspelningssessionen.
* Uppspelning och paus är aktiverat.
* Sökning tillåts inte. Om du vill söka, ringa `pause` för att avsluta tricks play-läge och sedan ringa `seek`.

* Du kan gå från trippelläge till tillåten uppspelningshastighet (uppspelning eller paus).
* När annonser har infogats i strömmen:

   * Du kan bara lura att spela medan du spelar huvudinnehållet. Ett fel skickas om du försöker byta för att lura till dig att spela under en annonsbrytning.
   * Efter att tricket har spelats upp ignoreras annonsbrytningar och inga annonshändelser utlöses.
   * Tidslinjen som visas av TVSDK för spelarprogrammet ändras inte även om annonsbrytningar hoppas över.
   * Det aktuella tidsvärdet hoppar framåt (snabbt framåt) eller bakåt (vid snabb tillbakaspolning) med varaktigheten för den överhoppade annonsbrytningen. Detta hoppbeteende för den aktuella tiden gör att strömmens varaktighet förblir oförändrad under trippelning. Spelarprogrammet kan hämta det lokala tidsvärdet för att spåra tiden i förhållande enbart till huvudinnehållet. Inga tidshopp utförs för de värden som returneras för lokal tid när en annons hoppas över.
   * The `MediaPlayerEvent.AD_BREAK_SKIPPED` -händelsen skickas omedelbart innan en annonsbrytning kommer att hoppas över. Spelaren kan använda den här händelsen för att implementera anpassad logik som är relaterad till de överhoppade annonsbrytningarna.
   * När du avslutar trick play anropas samma annonsuppspelningsprincip som när sökningen avslutas.

      Som vid sökning beror därför beteendet på om programmets uppspelningsprincip skiljer sig från standardinställningen. Som standard spelas den senast hoppade annonsbrytningen upp där du kommer ur trickläget.
