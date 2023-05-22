---
title: Minsta klientversion
description: Minsta klientversion
copied-description: true
exl-id: c4aebafe-33b4-4da3-9e79-53d6a7e9f22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Minsta klientversion {#minimum-client-version}

Adobe Primetime DRM 2.0.2 och senare innehåller vissa nya användningsregler som inte kan tolkas av Primetime DRM 2.0-klienter. Genom att ange den lägsta klientversion som stöds ( `HandlerConfiguration.setMinSupportedClientVersion()`) kan licensservern styra hur äldre klienter beter sig när de stöter på licenser med dessa användningsregler. Baserat på den här inställningen kan servern ange om äldre klienter kan ignorera de användningsregler de inte förstår eller om äldre klienter inte kan använda licenser med dessa användningsregler.

Till exempel:

* Om licensen anger kraven för enhetens funktioner ( [Enhetsfunktioner som krävs för att spela upp skyddat innehåll](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)) kan Primetime DRM-klienter 2.0.2 och senare tillämpa dessa krav.
* Om licensservern inte vill att innehållet ska spelas upp på klienter som inte förstår kraven för enhetsfunktioner ställer du in den lägsta klientversionen som stöds till 2 (för 2.0.2). Detta förhindrar servern från att utfärda licenser till Primetime DRM-klienter före 2.0.2. Den lägsta klientversionen gäller också om licensen överförs från en klient till en annan.
* Om licensservern vill tillåta äldre klienter att ignorera kraven på enhetsfunktioner anger du den lägsta klientversionen som stöds till 1 (för Primetime DRM 2.0). Servern utfärdar sedan en licens till valfri klientversion 2.0 eller senare. Om klienten uppgraderar eller överför licensen till en annan klient med version 2.0.2 eller senare, kommer kraven på enhetsfunktioner i licensen att gälla eftersom klienten då kan ge stöd för den regeln.
