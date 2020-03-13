---
seo-title: Adobe Pass och Adobe Access
title: Adobe Pass och Adobe Access
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adobe Pass och Adobe Access {#adobe-pass-and-adobe-access}

Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) ger autentisering och behörighet för användare/enheter i flera innehållsleverantörer. Användaren måste ha en giltig kabel-TV- eller satellit-TV-prenumeration.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass kan användas tillsammans med Adobe Access för att skydda medieinnehållet. I det här scenariot kan videospelaren (SWF) läsa in en annan SWF-fil som kallas *Access Enabler*, som hanteras av Adobe Systems. Med *Access Enabler* kan du ansluta till Adobe Pass-tjänsten och underlätta SAML SSO-integrering med identitetsleverantörssystem för MVPD (Multichannel Video Programming Distributor). Detta innebär att användarens webbläsare snabbt omdirigeras till inloggningssidan för MVPD, att en AuthN-token sparas och slutligen återgår till innehållswebbplatsen med en cachelagrad AuthN-session.

Då kan *Access Enabler* underlätta backend-auktoriseringar mellan Adobe Pass-tjänsten och MVPD. MVPD bevarar affärslogiken och avgör vilket innehåll användaren har rätt till. Behörigheten finns kvar i en ytterligare AuthZ-token för den innehållsresursen och skickas tillbaka till klienten.

Autentiserings- och auktoriseringstoken signeras med det unika ID:t och den privata nyckeln för Adobe Access-klienten för att undvika manipulering eller förfalskning. Denna token kan bara nås via *Access Enabler*.

Videospelaren kan starta processen genom att anropa `getAuthorization` Access Enabler **. När det finns giltiga AuthN/AuthZ-token skickar *AccessEnabler* ett återanrop till videospelaren som innehåller en kort medietoken för uppspelning av videoinnehållet.

Adobe Pass tillhandahåller ett Java-bibliotek för medietokenvalidator som kan distribueras till en server. När du använder Flash Access-servern för skydd av innehåll kan du integrera medietokenvalideraren med ett plugin-program på serversidan för att automatiskt utfärda en allmän licens efter att du har validerat medietoken. Innehållet direktuppspelas sedan från CDN-servrarna till klienten. Om du vill hämta en innehållslicens kan den kortlivade medietoken skickas till Adobe Access-servern där tokenens giltighet verifieras och en licens kan utfärdas.

Den långvariga AuthN-token används vanligtvis av *Access Enabler* för alla innehållsutvecklare för att representera AuthN för den MVPD-prenumeranten. Dessutom kan Adobe Access Server och Token Verifier hanteras av CDN eller en tjänsteleverantör för innehållsleverantörens räkning.
