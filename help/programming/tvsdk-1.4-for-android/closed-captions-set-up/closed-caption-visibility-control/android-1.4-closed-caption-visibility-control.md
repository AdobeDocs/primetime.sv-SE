---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
seo-description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
seo-title: Kontrollera synlighet för undertexter
title: Kontrollera synlighet för undertexter
uuid: 42913347-8158-474e-aa3c-ba4d38baba12
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Översikt {#control-closed-caption-visibility}

Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.

>[!TIP]
>
>Om undertextad text visas när spelaren går över till sökningsläget visas inte texten längre när sökningen har slutförts. Efter några sekunder visar i stället TVSDK nästa textning i videon efter den avslutande sökpositionen.

>[!NOTE]
>
>Synlighetsvärdena för undertexter definieras i `MediaPlayer.Visibility`. >
>
```java>
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. Vänta tills MediaPlayer har minst tillståndet PREPARED (se [Vänta på ett giltigt tillstånd](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Om du vill hämta den aktuella synlighetsinställningen för undertexter använder du metoden get i MediaPlayer, som returnerar ett synlighetsvärde.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Om du vill ändra synligheten för undertexter använder du metoden set och skickar ett synlighetsvärde från `MediaPlayer.Visibility`.

   Exempel:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

