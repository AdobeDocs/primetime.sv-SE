---
title: Minsta klientversion
description: Minsta klientversion
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Minsta klientversion {#minimum-client-version}

Adobe Access 2.0.2 och senare innehåller vissa nya användningsregler som inte kan tolkas av Adobe Access 2.0-klienter. Genom att ställa in den klientversion som stöds ( `HandlerConfiguration.setMinSupportedClientVersion()`) kan licensservern styra hur äldre klienter beter sig när de stöter på licenser med dessa användningsregler. Baserat på den här inställningen kan servern ange om äldre klienter kan ignorera de användningsregler de inte förstår eller om äldre klienter inte kan använda licenser med dessa användningsregler.

Exempel:

* Om licensen anger kraven för enhetsfunktioner ( [Enhetsfunktioner som krävs för att spela upp skyddat innehåll](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)) kan Adobe Access-klienter 2.0.2 och senare tillämpa dessa krav.
* Om licensservern inte vill att innehållet ska spelas upp på klienter som inte förstår kraven för enhetsfunktioner ställer du in den lägsta klientversionen som stöds till 2 (för 2.0.2). Detta förhindrar att servern utfärdar licenser till Adobe Access-klienter före 2.0.2. Den lägsta klientversionen används också om licensen överförs från en klient till en annan.
* Om licensservern vill att äldre klienter ska kunna ignorera enhetens funktionskrav anger du den lägsta klientversionen som stöds till 1 (för Adobe Access 2.0). Servern utfärdar en licens till alla klientversioner, version 2.0 eller senare. Om klienten uppgraderar eller överför licensen till en annan klient med version 2.0.2 eller senare, kommer kraven på enhetsfunktioner i licensen att gälla, eftersom klienten nu har stöd för den regeln.

