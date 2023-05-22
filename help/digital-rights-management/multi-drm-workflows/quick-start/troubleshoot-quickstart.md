---
description: Vanliga problem vid testning är ofta ExpressPlay-autentiserare, transportprotokoll och obligatoriska parametrar för serviceförfrågningar.
title: Felsökning av snabbstart
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Felsökning av snabbstart{#troubleshooting-your-quick-start}

Vanliga problem vid testning är ofta ExpressPlay-autentiserare, transportprotokoll och obligatoriska parametrar för serviceförfrågningar.

Om [!DNL curl] begäranden till ExpressPlay för att skapa token misslyckas, kommer svarstexten att innehålla ett felmeddelande som förklarar orsaken till felet.

Om tokengenereringen lyckas, men innehållet fortfarande inte spelas upp, kontrollerar du om det finns fel i loggarna för tokeninlösen för ExpressPlay, t.ex.&quot;Utgånen token&quot;.

Om tokengenereringen lyckades och inlösen inte hade något fel, men videon fortfarande inte spelas upp, kontrollerar du att CEK matchar innehållet och att innehållsformatet matchar målenhetens funktioner.

Dessutom:

* Kontrollera att du använder rätt kundautentiserare i dina serviceförfrågningar. Det är lätt att oavsiktligt använda produktionsautentiseraren när du ska använda testautentiseraren. Kontrollera också att du använder *din* autentiserare. Du kan till exempel låna någon annans `curl` och glöm att byta in din autentiserare mot deras.

* Kontrollera att du använder rätt transportprotokoll i dina förfrågningar eller i dina manifest ( `https://` kontra `https://`eller i fallet FairPlay, `skd://` kontra `https://` kontra `https://`.

* Se till att du inkluderar alla obligatoriska frågeparametrar för den DRM-lösning du arbetar med. Det är enkelt att växla mellan exempelvis PlayReady och Widewin eftersom de båda fungerar med DASH, men de obligatoriska parametrarna för begäran och paketeringskonfigurationerna skiljer sig åt.
* Bekräfta att ditt ExpressPlay-konto har tillräckligt många tokenkrediter och att det inte har tömts.
* Bekräfta att triplet med DRM-data som skickas till TVSDK är korrekt: ExpressPlay-token, licensserverns URL och DRM-typ.
* Kontrollera att alla dina komponenter antar samma sak om vilken ExpressPlay-miljö som används i två miljöer, Test och Production.
* Tänk på att olika webbläsare vanligtvis bara har stöd för en DRM för DASH-innehåll.
* Från och med TVSDK 2.4 stöds bara DASH-LIVE-paketeringsprofilen. (Stöd för DASH-OnDemand finns på färdplanen.)
* Stödet för AndroidTV PlayReady är tillfälligt på grund av begränsningar i enhetstillverkaren. För att ge exempel

   * Razer Forge-enheten har problem med PlayReady-innehåll
   * Amazon FireTV kan inte använda DASH-innehåll som har ljudspåret krypterat

* Från och med TVSDK 2.4 har endast AndroidTV-enheter vanligtvis stöd för både PlayReady och Widewin DRM. Alla andra Android-enheter har vanligtvis bara stöd för Widewin.
* Från och med TVSDK 2.4 kräver Android TVSDK för närvarande att PSSH-rutan finns i .mpd-manifestet. Detta strider mot DASH-standarden, som anger att PSSH-rutan kan vara var som helst, som i själva innehållet och inte bara i .mpd-filen.
