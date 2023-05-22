---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.
title: Kontrollera synlighet för undertexter
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

1. Använd `MediaPlayer.ccVisibility` för att komma åt den aktuella synlighetsinställningen för de stängda bildtexterna.
