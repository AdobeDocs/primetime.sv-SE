---
description: Du kan enkelt skapa ett anpassat användargränssnitt baserat på ramverket för referensimplementering.
seo-description: Du kan enkelt skapa ett anpassat användargränssnitt baserat på ramverket för referensimplementering.
seo-title: Skapa ett anpassat användargränssnitt
title: Skapa ett anpassat användargränssnitt
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Skapa ett anpassat användargränssnitt {#build-a-custom-user-interface}

Du kan skapa ett anpassat användargränssnitt baserat på ramverket för referensimplementering.

Gränssnittskomponenterna i följande funktioner är redan integrerade:

* Klickbara annonser
* Lägg till övertäckningar
* Ljud med låg bindning
* Undertexter
* Lyssnare för alla ovanstående komponenter

1. Redigera [!DNL PlayerFragment.java] filen för att initiera de gränssnittskomponenter som du vill använda i spelaren.

1. Redigera [!DNL res/player/player_fragment.xml] filen för att anpassa användargränssnittet.
1. Bygg projektet.

>[!NOTE]
>
>Om du vill göra gränssnittsändringar i sökfältet kan du redigera klassen MarkableSeekBar. Klassen [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) hanterar skjutreglaget, reglagets reglage, markörhållare, cue-markörer, buffertintervall och bakgrunder för sökintervall.