---
description: Du kan styra synligheten för undertexter. När synlighet har aktiverats visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
seo-description: Du kan styra synligheten för undertexter. När synlighet har aktiverats visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
seo-title: Kontrollera synlighet för undertexter
title: Kontrollera synlighet för undertexter
uuid: b9d48d70-2554-4948-8654-fa45093c3782
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '206'
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

1. Vänta tills `MediaPlayer` statusen PREPARED är minst.

   Mer information finns i ui-state-prepare-wait-for.
1. Om du vill hämta den aktuella synlighetsinställningen för undertexter använder du get-metoden i `MediaPlayer`, som returnerar ett synlighetsvärde.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Om du vill ändra synligheten för undertexter använder du metoden set och skickar ett synlighetsvärde från `MediaPlayer.Visibility`.

   Exempel:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```

