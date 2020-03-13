---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-title: Välj ett aktuellt bildtextspår bland tillgängliga spår
title: Välj ett aktuellt bildtextspår bland tillgängliga spår
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Översikt {#work-with-closed-captions}

Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.

Undertexter är vanligtvis på samma språk som ljudet och visar även bakgrundsljud som text, men underrubriker är vanligtvis på ett annat språk och inkluderar inte bakgrundsljud.

TVSDK har stöd för återgivning av följande format:

* 608 och 708 undertexter, när de levereras som en del av videotransportströmmen över HLS som datapaket i MPEG-2-videoströmmar.
* WebVTT-beskrivningsfiler, som refereras från M3U8-manifestfiler enligt definitionen i HLS-specifikationerna. De är automatiskt tillgängliga som textningsspår i Primetime-spelaren.

Du kan:

* Välj ett tillgängligt bildtextspår som aktuellt spår och lyssna efter händelser som indikerar ytterligare tillgängliga spår.
* Aktivera eller inaktivera undertextning (synlig eller inte synlig) med hjälp av `MediaPlayer` gränssnittet.
* Välj formatalternativ som anger hur undertexter återges av den underliggande videomotorn. Använd `MediaPlayerItem` gränssnittet för att välja format som teckensnitt eller teckenfärg.
