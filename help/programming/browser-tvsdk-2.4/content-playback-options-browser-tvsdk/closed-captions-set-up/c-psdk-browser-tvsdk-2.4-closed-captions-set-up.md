---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-title: Arbeta med undertexter
title: Arbeta med undertexter
uuid: bc069e04-3ea3-4cdf-a8a6-d8aef91ece91
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Arbeta med undertexter{#work-with-closed-captions}

Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.

Undertexter är vanligtvis på samma språk som ljudet och visar även bakgrundsljud som text, men underrubriker är vanligtvis på ett annat språk och inkluderar inte bakgrundsljud.

Webbläsarens TVSDK har stöd för återgivning av följande format:

* 608 och 708 undertexter, när de levereras som en del av videotransportströmmen över HLS som datapaket i MPEG-2-videoströmmar.
* WebVTT-beskrivningsfiler, som refereras från M3U8-manifestfiler enligt definitionen i HLS-specifikationerna. De är automatiskt tillgängliga som textningsspår i Primetime-spelaren.

Du kan:

* Välj ett tillgängligt bildtextspår som aktuellt spår och lyssna efter händelser som indikerar ytterligare tillgängliga spår.
* Aktivera eller inaktivera undertextning (synlig eller inte synlig) med hjälp av `MediaPlayer` gränssnittet.
* Välj formatalternativ som anger hur undertexter återges av den underliggande videomotorn. Använd `MediaPlayerItem` gränssnittet för att välja format som teckensnitt eller teckenfärg.

