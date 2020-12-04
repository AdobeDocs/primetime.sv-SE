---
seo-title: Adobe Primetime-autentisering och Adobe Primetime DRM
title: Adobe Primetime-autentisering och Adobe Primetime DRM
uuid: 44fe3956-efb5-4fc5-97e2-37abb6554322
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Adobe Primetime-autentisering och Adobe Primetime DRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

Adobe Primetime-autentisering ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) ger användar-/enhetsautentisering och behörighet för flera innehållsleverantörer. Användaren måste ha en giltig kabel-TV- eller satellit-TV-prenumeration.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Primetime-autentisering kan användas tillsammans med Adobe Primetime DRM för att skydda medieinnehållet. I det här scenariot kan videospelaren (SWF) läsa in en annan SWF-fil som kallas *Åtkomstaktiveraren*, som finns hos Adobe Systems. *Access Enabler* används för att ansluta till Adobe Primetime autentiseringstjänst och underlätta SAML SSO-integrering med identitetsleverantörssystem för MVPD (Multichannel Video Programming Distributor). Detta innebär att användarens webbläsare snabbt omdirigeras till inloggningssidan för MVPD, att en AuthN-token sparas och slutligen återgår till innehållswebbplatsen med en cachelagrad AuthN-session.

*Åtkomstaktiveraren* kan sedan underlätta backend-auktoriseringar mellan Adobe Primetime autentiseringstjänst och MVPD. MVPD bevarar affärslogiken och avgör vilket innehåll användaren har rätt till. Behörigheten finns kvar i en ytterligare AuthZ-token för den innehållsresursen och skickas tillbaka till klienten.

Autentiserings- och auktoriseringstoken signeras med det unika ID:t och den privata nyckeln för Primetime DRM-klienten för att undvika manipulering eller förfalskning. Denna token kan bara nås via *Access Enabler*.

Videospelaren kan utlösa processen genom att anropa `getAuthorization` på *Access Enabler*. När det finns giltiga AuthN/AuthZ-tokens skickar *AccessEnabler* ett återanrop till videospelaren som innehåller en kort medietoken för uppspelning av videoinnehållet.

Adobe Primetime-autentisering ger ett Java-bibliotek för medietoken som kan distribueras till en server. När du använder Primetime DRM-servern för innehållsskydd kan du integrera medietokenvalidatorn med ett plugin-program på servern Primetime för att automatiskt utfärda en generisk licens efter att du har validerat medietoken. Innehållet direktuppspelas sedan från CDN-servrarna till klienten. Om du vill hämta en innehållslicens kan den kortlivade medietoken skickas till Primetimes DRM-server, där tokenens giltighet verifieras och en licens kan utfärdas.

Den långvariga AuthN-token används vanligtvis av *Access Enabler* för alla innehållsutvecklare för att representera AuthN för den MVPD-prenumeranten. Dessutom kan Primetime DRM-servern och tokenverifieraren hanteras av CDN eller en tjänsteleverantör för innehållsleverantörens räkning.