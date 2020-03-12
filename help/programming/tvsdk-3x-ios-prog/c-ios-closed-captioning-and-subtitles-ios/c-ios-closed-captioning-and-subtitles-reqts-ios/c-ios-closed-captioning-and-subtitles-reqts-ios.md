---
description: Undertexter och undertexter har vissa unika skillnader och du kan aktivera dem på olika sätt.
seo-description: Undertexter och undertexter har vissa unika skillnader och du kan aktivera dem på olika sätt.
seo-title: Krav för undertexter och undertexter
title: Krav för undertexter och undertexter
uuid: 18ed6ac1-4b25-4590-8c61-3ffb0464d093
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

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

      Huvudinnehållet och annonserna `PTMediaPlayer` spelas upp, där huvudinnehållet kan vara live/linear eller VOD, och annonserna kan vara pre-roll, mid-roll eller post-roll.
   Nedan följer några ytterligare krav för undertexter i iOS:

   * För tidsstämplar måste `X-TIMESTAMP-MAP` `WebVTT` värdet, som anges i filens sidhuvud, matcha videons tidsstämpel.

   * För systemet måste du använda iOS 6.1 eller senare.


>[!IMPORTANT]
>
>Kraven för undertexter gäller inte för undertexter.