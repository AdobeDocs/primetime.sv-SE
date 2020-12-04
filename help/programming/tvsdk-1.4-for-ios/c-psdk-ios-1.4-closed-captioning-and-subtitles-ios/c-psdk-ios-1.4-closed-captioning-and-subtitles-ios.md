---
description: Undertexter och undertexter har vissa unika skillnader och du kan aktivera dem på olika sätt.
seo-description: Undertexter och undertexter har vissa unika skillnader och du kan aktivera dem på olika sätt.
seo-title: Undertexter och undertexter
title: Undertexter och undertexter
uuid: 91daf0be-087a-4be5-86c2-f8b83da43a8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '243'
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

      `PTMediaPlayer` spelar upp huvudinnehållet och annonserna, där huvudinnehållet kan vara live/linear eller VOD, och annonserna kan vara pre-roll, mid-roll eller post-roll.
   Nedan följer några ytterligare krav för undertexter i iOS:

   * För tidsstämplar måste `X-TIMESTAMP-MAP`-värdet, som anges i rubrikavsnittet i `WebVTT`-filen, matcha videotidsstämpeln.

   * För systemet måste du använda iOS 6.1 eller senare.


>[!IMPORTANT]
>
>Kraven för undertexter gäller inte för undertexter.

