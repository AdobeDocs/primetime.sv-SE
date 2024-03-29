---
description: Ibland kan det hända att innehållet inte kan spelas upp. Ett obegränsat antal situationer kan orsaka detta, bland annat fel i webbläsarens nätverksstack, transportlager, operativsystem, Flashens Player körningsmiljö eller Primetimes DRM-system.
title: Översikt över testfel
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Fel vid testning {#triaging-errors}

Ibland kan det hända att innehållet inte kan spelas upp. Ett obegränsat antal situationer kan orsaka detta, bland annat fel i webbläsarens nätverksstack, transportlager, operativsystem, Flashens Player körningsmiljö eller Primetimes DRM-system.

Det första diagnostiska steget är att avgöra om problemet visar sig utan DRM-kryptering som introducerats i ekvationen. Försök att paketera innehållet, men instruera paketeraren att inte kryptera innehållet. Om problemet kvarstår är det troligen ett problem med kodning eller paketering av innehållet, eller någonstans i nätverksinfrastrukturen. Om problemet försvinner när innehållet paketeras utan kryptering beror det troligtvis på ett DRM-problem, och du bör trimma klient/server.

Primetime DRM (utanför Primetime Cloud DRM) har funnits på marknaden i flera år. Därför finns det gott om information från användarna om felsökning och konfigurering av Primetime DRM. Adobe har skapat ett forum där Primetimes DRM-användare (tidigare kallat Adobe Access) kan samla in och dela problem och lösningar. Kontrollera om ditt problem har diskuterats tidigare: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Klientfelsökning {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

Om innehållet inte spelas upp bör du gå igenom panelen till höger i Exempelvideouppspelarna där alla `DRMErrorEvent` som inträffar. Om det finns en felhändelse korrelerar den med ett av Flashens Player körningsfel:

* [Felmeddelandereferens för DRM-klient](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)eller
* [Körningsfel för AS3-Flash](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM-problem börjar vid 3 300)
