---
description: Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.
title: Arbeta med undertexter
exl-id: 7550ef78-e87f-4cbc-91d6-9aab39e613d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Arbeta med undertexter{#work-with-closed-captions}

Textning för hörselskadade visar ljudet i en video som text på skärmen när ljudet inte kan höras eller när tittaren inte hörs.

Undertexter är vanligtvis på samma språk som ljudet och visar även bakgrundsljud som text, men underrubriker är vanligtvis på ett annat språk och inkluderar inte bakgrundsljud.

TVSDK har stöd för återgivning av följande format:

* 608 och 708 undertexter, när de levereras som en del av videotransportströmmen över HLS som datapaket i MPEG-2-videoströmmar.
* WebVTT-beskrivningsfiler, som refereras från M3U8-manifestfiler enligt definitionen i HLS-specifikationerna. De är automatiskt tillgängliga som textningsspår i Primetime-spelaren.

Du kan:

* Välj ett tillgängligt bildtextspår som aktuellt spår och lyssna efter händelser som indikerar ytterligare tillgängliga spår.
* Aktivera eller inaktivera undertextning (synlig eller inte synlig) med `MediaPlayer` gränssnitt.
* Välj formatalternativ som anger hur undertexter återges av den underliggande videomotorn. Använd `MediaPlayerItem` för att välja format som teckensnitt eller teckenfärg.
