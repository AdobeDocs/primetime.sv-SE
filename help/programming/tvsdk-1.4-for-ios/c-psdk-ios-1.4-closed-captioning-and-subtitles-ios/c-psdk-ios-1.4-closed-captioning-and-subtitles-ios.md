---
description: Undertexter och undertexter har vissa unika skillnader och du kan aktivera dem på olika sätt.
title: Undertexter och undertexter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Krav för undertexter och undertexter {#requirements-for-subtitles-and-closed-captions}

Undertexter och undertexter har vissa unika skillnader och du kan aktivera dem på olika sätt.

Undertextströmmar körs parallellt med huvudinnehållet. Textning ingår i MPEG-2-videoströmmens datapaket.

Du bör vara medveten om följande krav för undertexter och undertexter:

* **Undertexter**

   * Undertexter är vanligtvis på samma språk som ljudet och motsvarar även bakgrundsljud som text.
   * Undertexter ingår i datapaketen för MPEG-2-videoströmmarna i videoöverföringsströmmen.
   * Undertexter stöds i den omfattning som tillhandahålls av ramverket AV Foundation.

* **Undertexter**

   * Undertexter finns vanligtvis på ett annat språk och innehåller inte bakgrundsljud.
   * Undertexter finns i strömmar som körs parallellt med huvudinnehållet.

     The `PTMediaPlayer` spelar upp huvudinnehållet och annonserna, där huvudinnehållet kan vara live/linear eller VOD, och där annonserna kan vara pre-roll, mid-roll eller post-roll.

  Nedan följer ytterligare krav för undertexter i iOS:

   * För tidsstämplar är `X-TIMESTAMP-MAP` värde, som anges i rubrikavsnittet i `WebVTT` måste matcha videons tidsstämpel.

   * För systemet måste du använda iOS 6.1 eller senare.

>[!IMPORTANT]
>
>Kraven för undertexter gäller inte för undertexter.
