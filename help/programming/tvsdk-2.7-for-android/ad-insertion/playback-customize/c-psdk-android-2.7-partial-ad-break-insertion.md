---
title: Insättning av delvis annonsradbrytning
description: Insättning av delvis annonsradbrytning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Insättning av delvis annonsradbrytning {#partial-ad-break-insertion}

Du kan aktivera en TV-liknande upplevelse genom att kunna vara med mitt i en annons i liveströmmar. Med funktionen för partiell annonsbrytning kan du efterlikna en TV-liknande upplevelse där klienten, om den startar en liveström inuti en mikrofon, kommer att börja i den där mikrofonen. Det liknar en övergång till en TV-kanal och reklamen fungerar smidigt.

Om en användare till exempel går med mitt i en 90-sekunders annonsbrytning (tre 30-sekunders annonser), tio sekunder in i den andra annonsen (det vill säga 40 sekunder in i annonsbrytningen) händer följande:

* Den andra annonsen spelas upp för den återstående längden (20 sek) följt av den tredje annonsen.
* Annonsspårare för annonsen som spelas delvis (den andra annonsen) utlöses inte. Bara spåraren för den tredje annonsen aktiveras.

Det här beteendet är inte aktiverat som standard. Så här aktiverar du den här funktionen i din app:

1. Inaktivera live-föranrop med AdvertisingMetadata-klassens setEnableLivePreroll-metod.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Aktivera inställningen för delvis infogning av annonsradbrytning. Använd den nya metoden setPartialAdBreakPref i MediaPlayer-gränssnittet för att aktivera den här funktionen. Använd metoden getPartialAdBreakPref för att hitta det aktuella läget för den här inställningen.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

