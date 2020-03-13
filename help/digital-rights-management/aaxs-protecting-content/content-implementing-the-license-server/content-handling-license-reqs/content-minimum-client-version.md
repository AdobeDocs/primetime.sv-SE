---
seo-title: Minsta klientversion
title: Minsta klientversion
uuid: 9f39e4e7-64eb-43ea-b194-b744838a411e
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Minsta klientversion {#minimum-client-version}

Adobe Access 2.0.2 och senare innehåller vissa nya användningsregler som inte kan tolkas av Adobe Access 2.0-klienter. Genom att ange den klientversion som stöds `HandlerConfiguration.setMinSupportedClientVersion()`så lite som möjligt kan licensservern styra hur äldre klienter beter sig när de stöter på licenser med dessa användningsregler. Baserat på den här inställningen kan servern ange om äldre klienter kan ignorera de användningsregler de inte förstår eller om äldre klienter inte kan använda licenser med dessa användningsregler.

Exempel:

* Om licensen anger kraven för enhetsfunktioner ( [enhetsfunktioner som krävs för att spela upp skyddat innehåll](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)) kan Adobe Access-klienter 2.0.2 och senare tillämpa dessa krav.
* Om licensservern inte vill att innehållet ska spelas upp på klienter som inte förstår kraven för enhetsfunktioner ställer du in den lägsta klientversionen som stöds till 2 (för 2.0.2). Detta förhindrar servern från att utfärda licenser till Adobe Access-klienter före 2.0.2. Den lägsta klientversionen används också om licensen överförs från en klient till en annan.
* Om licensservern vill tillåta äldre klienter att ignorera kraven på enhetsfunktioner anger du den lägsta klientversionen som stöds till 1 (för Adobe Access 2.0). Servern utfärdar en licens till alla klientversioner, version 2.0 eller senare. Om klienten uppgraderar eller överför licensen till en annan klient med version 2.0.2 eller senare, kommer kraven på enhetsfunktioner i licensen att gälla, eftersom klienten nu har stöd för den regeln.

