---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.
title: Kontrollera synlighet för undertexter
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Kontrollera synlighet för undertexter{#control-closed-caption-visibility}

Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.

>[!TIP]
>
>Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.

Om undertextad text visas när spelaren går till sökningsläget visas inte texten när sökningen är klar. Efter några sekunder visar webbläsaren TVSDK i stället nästa textning i videon efter sökpositionen.

>[!TIP]
>
>Synlighetsvärdena för undertexter styrs med `MediaPlayer.VISIBLE` och `MediaPlayer.INVISIBLE`.

1. Använd egenskapen `MediaPlayer.ccVisibility` för att komma åt den aktuella synlighetsinställningen för de stängda bildtexterna.

