---
description: I det här avsnittet finns en konceptuell översikt över konfiguration, alternativ och innebörd för skydd av utdata.
seo-description: I det här avsnittet finns en konceptuell översikt över konfiguration, alternativ och innebörd för skydd av utdata.
seo-title: RBOP-begrepp
title: RBOP-begrepp
uuid: fc19c3c9-39a1-4b62-b763-101e5454a01f
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# RBOP-begrepp {#rbop-concepts}

I det här avsnittet finns en konceptuell översikt över konfiguration, alternativ och innebörd för skydd av utdata.

Du anger dina upplösningsbaserade krav för utdataskydd i en hierarkisk JSON-struktur. *Utdatakraven är pixelbaserade.*

På den högsta nivån i JSON-specifikationen kan du definiera maximal pixelupplösning och pixelbegränsningar för angivna upplösningar:

* `maxPixel` - Den maximala pixelupplösningen definierar den maximala upplösning som dekrypteringen gäller.
* `pixelConstraints` - Pixelbegränsningar definierar utdatakrav som måste framtvingas för en angiven upplösning.

Du kopplar utdatakrav till specifika pixelbegränsningar. De typer av krav som du kan koppla till en viss pixelbegränsning är bl.a. begränsningar för digitala, analoga och OTA-anslutningar (over-the-air).

**Digital Output**

Kravet på digitala utdata kan ange restriktiva alternativ, t.ex.&quot;digitalt utdataskydd krävs&quot; eller&quot;uppspelning tillåts inte&quot;. Utdatakraven kan även specificera mindre begränsande alternativ som&quot;inget skydd bör tillämpas&quot; eller&quot;digitalt skydd bör användas om det finns tillgängligt&quot;.

**Analoga utdata**

Analoga utdataanslutningar är enklare än digitala utdata. De består av ett enda produktionskrav.
