---
description: I det här avsnittet finns en konceptuell översikt över konfiguration, alternativ och innebörd för skydd av utdata.
title: RBOP-begrepp
exl-id: 5b9de292-e060-467d-beca-5f428e45ed69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# RBOP-begrepp {#rbop-concepts}

I det här avsnittet finns en konceptuell översikt över konfiguration, alternativ och innebörd för skydd av utdata.

Du anger dina upplösningsbaserade krav för utdataskydd i en hierarkisk JSON-struktur. *Utdatakraven är pixelbaserade.*

På den högsta nivån i JSON-specifikationen kan du definiera maximal pixelupplösning och pixelbegränsningar för angivna upplösningar:

* `maxPixel` - Den maximala pixelupplösningen definierar den maximala upplösning som dekrypteringen gäller.
* `pixelConstraints` - Pixelbegränsningar definierar utdatakrav som måste framtvingas för en angiven upplösning.

Du kopplar utdatakrav till specifika pixelbegränsningar. De typer av krav som du kan koppla till en viss pixelbegränsning är bl.a. begränsningar för digitala, analoga och OTA-anslutningar (over-the-air).

**Digital Output**

Kravet på digitala utdata kan ange restriktiva alternativ, t.ex.&quot;digitalt utdataskydd krävs&quot; eller&quot;uppspelning tillåts inte&quot;. Utdatakraven kan även specificera mindre restriktiva alternativ, till exempel&quot;inget skydd bör tillämpas&quot; eller&quot;digitalt skydd bör användas om det är tillgängligt&quot;.

**Analoga utdata**

Analoga utdataanslutningar är enklare än digitala utdata. De består av ett enda produktionskrav.
