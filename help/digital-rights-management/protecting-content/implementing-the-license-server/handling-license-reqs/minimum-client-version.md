---
seo-title: Minsta klientversion
title: Minsta klientversion
uuid: f2b56cff-96fa-4954-a08a-9b3e78f496d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Minsta klientversion {#minimum-client-version}

Adobe Primetime DRM 2.0.2 och senare innehåller vissa nya användningsregler som inte kan tolkas av Primetime DRM 2.0-klienter. Genom att ange den klientversion som stöds `HandlerConfiguration.setMinSupportedClientVersion()`så lite som möjligt kan licensservern styra hur äldre klienter beter sig när de stöter på licenser med dessa användningsregler. Baserat på den här inställningen kan servern ange om äldre klienter kan ignorera de användningsregler de inte förstår eller om äldre klienter inte kan använda licenser med dessa användningsregler.

Exempel:

* Om licensen anger kraven för enhetsfunktioner ( [enhetsfunktioner som krävs för att spela upp skyddat innehåll](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)) kan Primetime DRM-klienter 2.0.2 och senare tillämpa dessa krav.
* Om licensservern inte vill att innehållet ska spelas upp på klienter som inte förstår kraven för enhetsfunktioner ställer du in den lägsta klientversionen som stöds till 2 (för 2.0.2). Detta förhindrar servern från att utfärda licenser till Primetime DRM-klienter före 2.0.2. Den lägsta klientversionen gäller också om licensen överförs från en klient till en annan.
* Om licensservern vill tillåta äldre klienter att ignorera kraven på enhetsfunktioner anger du den lägsta klientversionen som stöds till 1 (för Primetime DRM 2.0). Servern utfärdar sedan en licens till valfri klientversion 2.0 eller senare. Om klienten uppgraderar eller överför licensen till en annan klient med version 2.0.2 eller senare, kommer kraven på enhetsfunktioner i licensen att gälla eftersom klienten då kan ge stöd för den regeln.

