---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.
seo-description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret.
seo-title: Kontrollera synlighet för undertexter
title: Kontrollera synlighet för undertexter
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '143'
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

