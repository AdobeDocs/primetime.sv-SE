---
description: Vanliga problem vid testning är ofta ExpressPlay-autentiserare, transportprotokoll och obligatoriska parametrar för serviceförfrågningar.
seo-description: Vanliga problem vid testning är ofta ExpressPlay-autentiserare, transportprotokoll och obligatoriska parametrar för serviceförfrågningar.
seo-title: Felsökning av snabbstart
title: Felsökning av snabbstart
uuid: 42256aa0-2efc-4602-aefc-3bab2dc58ec0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Felsöka snabbstart{#troubleshooting-your-quick-start}

Vanliga problem vid testning är ofta ExpressPlay-autentiserare, transportprotokoll och obligatoriska parametrar för serviceförfrågningar.

Om dina [!DNL curl]-begäranden till ExpressPlay för token-generering misslyckas innehåller svarstexten ett felmeddelande som förklarar orsaken till felet.

Om tokengenereringen lyckas, men innehållet fortfarande inte spelas upp, kontrollerar du om det finns fel i loggarna för tokeninlösen för ExpressPlay, t.ex.&quot;Utgånen token&quot;.

Om tokengenereringen lyckades och inlösen inte hade något fel, men videon fortfarande inte spelas upp, kontrollerar du att CEK matchar innehållet och att innehållsformatet matchar målenhetens funktioner.

Dessutom:

* Kontrollera att du använder rätt kundautentiserare i dina serviceförfrågningar. Det är lätt att oavsiktligt använda produktionsautentiseraren när du ska använda testautentiseraren. Kontrollera också att du använder *din*-autentiserare. Under testningen kan du till exempel låna någon annans `curl`-kommando och glömma att byta in autentiseraren för sin.

* Kontrollera att du använder rätt transportprotokoll i dina förfrågningar eller i dina manifest ( `https://` jämfört med `https://`, eller i fallet FairPlay, `skd://` jämfört med `https://` jämfört med `https://`.

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

