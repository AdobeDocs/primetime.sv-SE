---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.
title: Kontrollera synlighet för undertexter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Kontrollera synlighet för undertexter{#control-closed-caption-visibility}

Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.

>[!TIP]
>
>Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.

Om undertextad text visas när spelaren går till sökningsläget visas inte texten när sökningen är klar. Efter några sekunder visar webbläsaren TVSDK i stället nästa textning i videon efter den avslutande sökpositionen.

>[!TIP]
>
>Synlighetsvärdena för undertexter styrs med `MediaPlayer.VISIBLE` och `MediaPlayer.INVISIBLE`.

1. Använd `MediaPlayer.ccVisibility` för att komma åt den aktuella synlighetsinställningen för de stängda bildtexterna.
