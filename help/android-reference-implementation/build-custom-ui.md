---
description: Du kan enkelt skapa ett anpassat användargränssnitt baserat på ramverket för referensimplementering.
title: Skapa ett anpassat användargränssnitt
exl-id: 96008010-cd63-4fb1-a3fc-2fc94b624413
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Skapa ett anpassat användargränssnitt {#build-a-custom-user-interface}

Du kan skapa ett anpassat användargränssnitt baserat på ramverket för referensimplementering.

Gränssnittskomponenterna i följande funktioner är redan integrerade:

* Klickbara annonser
* Lägg till övertäckningar
* Ljud med låg bindning
* Undertexter
* Lyssnare för alla ovanstående komponenter

1. Redigera [!DNL PlayerFragment.java] för att initiera de UI-komponenter som du vill använda i spelaren.

1. Redigera [!DNL res/player/player_fragment.xml] -fil för att anpassa användargränssnittet.
1. Bygg projektet.

>[!NOTE]
>
>Om du vill göra gränssnittsändringar i sökfältet kan du redigera klassen MarkableSeekBar. The [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) -klassen hanterar skjutreglaget, reglagets reglage, markörhållare, cue-markörer, buffertintervall och sökintervallbakgrunder.
