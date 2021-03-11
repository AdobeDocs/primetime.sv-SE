---
description: Du kan enkelt skapa ett anpassat användargränssnitt baserat på ramverket för referensimplementering.
title: Skapa ett anpassat användargränssnitt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

1. Redigera [!DNL PlayerFragment.java]-filen för att initiera de gränssnittskomponenter som du vill använda i spelaren.

1. Redigera [!DNL res/player/player_fragment.xml]-filen för att anpassa användargränssnittet.
1. Bygg projektet.

>[!NOTE]
>
>Om du vill göra gränssnittsändringar i sökfältet kan du redigera klassen MarkableSeekBar. Klassen [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) hanterar skjutreglaget, skjutreglagets reglage, markörhållare, cue-markörer, buffertintervall och sökintervallbakgrunder.