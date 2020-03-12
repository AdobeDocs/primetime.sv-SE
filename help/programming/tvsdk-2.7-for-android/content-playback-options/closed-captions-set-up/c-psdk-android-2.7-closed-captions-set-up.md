---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
seo-title: Arbeta med undertexter
title: Arbeta med undertexter
uuid: 6e105316-a166-45c1-b6b0-70c89c97c297
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Översikt {#work-with-closed-captions-overview}

Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.

Undertexter är vanligtvis på samma språk som ljudet och visar även bakgrundsljud som text, men underrubriker är vanligtvis på ett annat språk och inkluderar inte bakgrundsljud.

TVSDK har stöd för återgivning av följande format:

* 608 och 708 undertexter, när de levereras som en del av videotransportströmmen över HLS som datapaket i MPEG-2-videoströmmar.
* WebVTT-beskrivningsfiler, som refereras från M3U8-manifestfiler enligt definitionen i HLS-specifikationerna.

   Dessa filer är automatiskt tillgängliga som textningsspår i Primetime-spelaren.

Du kan göra följande:

* Välj ett tillgängligt bildtextspår som aktuellt spår och lyssna efter händelser som indikerar ytterligare tillgängliga spår.
* Aktivera (synlig) eller inaktivera (inte synlig) undertextning med hjälp av `MediaPlayer` gränssnittet.
* Välj formatalternativ som anger hur undertexter återges av den underliggande videomotorn.

   Använd `MediaPlayerItem` gränssnittet för att välja format som teckensnitt eller teckenfärg.

