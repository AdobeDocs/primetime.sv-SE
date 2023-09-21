---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
title: Arbeta med undertexter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Ökning {#work-with-closed-captions-overview}

Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.

Undertexter är vanligtvis på samma språk som ljudet och visar även bakgrundsljud som text, men underrubriker är vanligtvis på ett annat språk och inkluderar inte bakgrundsljud.

TVSDK har stöd för återgivning av följande format:

* 608 och 708 undertexter, när de levereras som en del av videotransportströmmen över HLS som datapaket i MPEG-2-videoströmmar.
* WebVTT-beskrivningsfiler, som refereras från M3U8-manifestfiler enligt definitionen i HLS-specifikationerna.

  Dessa filer är automatiskt tillgängliga som textningsspår i Primetime-spelaren.

Du kan göra följande:

* Välj ett tillgängligt bildtextspår som aktuellt spår och lyssna efter händelser som indikerar ytterligare tillgängliga spår.
* Aktivera (synlig) eller inaktivera (inte synlig) undertextning med `MediaPlayer` gränssnitt.
* Välj formatalternativ som anger hur undertexter återges av den underliggande videomotorn.

  Använd `MediaPlayerItem` för att välja format som teckensnitt eller teckensnittsfärg.
