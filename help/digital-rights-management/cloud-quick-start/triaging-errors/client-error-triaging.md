---
description: Ibland kan det hända att innehållet inte kan spelas upp. Ett obegränsat antal situationer kan orsaka detta, bland annat fel i webbläsarens nätverksstack, transportlager, operativsystem, Flash Player-körning eller Primetime DRM-system.
seo-description: Ibland kan det hända att innehållet inte kan spelas upp. Ett obegränsat antal situationer kan orsaka detta, bland annat fel i webbläsarens nätverksstack, transportlager, operativsystem, Flash Player-körning eller Primetime DRM-system.
seo-title: Översikt över testfel
title: Översikt över testfel
uuid: 44b4ab0e-5f08-44b0-bcb5-a869f6add69b
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Fel vid testning {#triaging-errors}

Ibland kan det hända att innehållet inte kan spelas upp. Ett obegränsat antal situationer kan orsaka detta, bland annat fel i webbläsarens nätverksstack, transportlager, operativsystem, Flash Player-körning eller Primetime DRM-system.

Det första diagnostiska steget är att avgöra om problemet visar sig utan DRM-kryptering som introducerats i ekvationen. Försök att paketera innehållet, men instruera paketeraren att inte kryptera innehållet. Om problemet kvarstår är det troligen ett problem med kodning eller paketering av innehållet, eller någonstans i nätverksinfrastrukturen. Om problemet försvinner när innehållet paketeras utan kryptering beror det troligtvis på ett DRM-problem, och du bör trimma klient/server.

Primetime DRM (utanför Primetime Cloud DRM) har funnits på marknaden i flera år. Därför finns det gott om information från användarna om felsökning och konfigurering av Primetime DRM. Adobe har tagit fram ett forum där Primetimes DRM-användare (tidigare kallat Adobe Access) kan samla in och dela problem och lösningar. Kontrollera om ditt problem har diskuterats tidigare: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Klientfelsökning {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Om innehållet inte spelas upp bör du gå igenom panelen till höger i Exempelvideouppspelaren, som loggar allt som `DRMErrorEvent` händer. Om det finns en felhändelse korrelerar den med ett av körningsfelen i Flash Player:

* [Felmeddelandereferens](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)för DRM-klient; eller
* [AS3 Flash-körningsfel](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM-problem börjar med 3300)

