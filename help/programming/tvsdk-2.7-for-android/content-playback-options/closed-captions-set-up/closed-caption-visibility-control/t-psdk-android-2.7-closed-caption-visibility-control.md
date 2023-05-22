---
description: Du kan styra synligheten för undertexter. När synlighet har aktiverats visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
title: Kontrollera synlighet för undertexter
exl-id: 358e32d8-7a3b-42bd-900b-dafe8eae3edf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Översikt {#control-closed-caption-visibility-overview}

Du kan styra synligheten för undertexter. När synlighet har aktiverats visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.

>[!TIP]
>
>Om undertextad text visas när spelaren går till sökläge visas inte texten längre när sökningen är klar. Efter några sekunder visar i stället TVSDK nästa textning i videon efter den avslutande sökpositionen.
>
>Synlighetsvärdena för undertexter definieras i `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Vänta på `MediaPlayer` vara i åtminstone statusen FÖRBEREDD.

   Mer information finns i ui-state-prepare-wait-for.
1. Använd metoden get i för att hämta den aktuella synlighetsinställningen för undertexter `MediaPlayer`, som returnerar ett synlighetsvärde.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Om du vill ändra synligheten för undertexter använder du metoden set och skickar ett synlighetsvärde från `MediaPlayer.Visibility`.

   Till exempel:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
