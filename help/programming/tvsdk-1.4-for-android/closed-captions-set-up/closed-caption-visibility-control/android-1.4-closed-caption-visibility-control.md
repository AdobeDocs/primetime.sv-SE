---
description: Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.
title: Kontrollera synlighet för undertexter
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Översikt {#control-closed-caption-visibility}

Du kan styra synligheten för undertexter. När synligheten är aktiverad visas det markerade spåret. Om du ändrar vilket spår som är aktuellt ändras inte synlighetsinställningen.

>[!TIP]
>
>Om undertextad text visas när spelaren går över till sökningsläget visas inte texten längre när sökningen har slutförts. Efter några sekunder visar i stället TVSDK nästa textning i videon efter den avslutande sökpositionen.

>[!NOTE]
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

1. Vänta tills MediaPlayer har minst tillståndet PREPARED (se [Vänta på ett giltigt tillstånd](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Om du vill hämta den aktuella synlighetsinställningen för undertexter använder du metoden get i MediaPlayer, som returnerar ett synlighetsvärde.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Om du vill ändra synligheten för undertexter använder du metoden set och skickar ett synlighetsvärde från `MediaPlayer.Visibility`.

   Till exempel:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
