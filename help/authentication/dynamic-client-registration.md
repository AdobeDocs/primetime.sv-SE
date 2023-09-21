---
title: Dynamisk klientregistrering
description: Dynamisk klientregistrering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Dynamisk klientregistrering {#dynamic-client-registration}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Kontext {#context}

För att anpassa sig till moderna säkerhetsrutiner, förbättrad användarupplevelse och krav på plattformsägare går Adobe Primetime Authentication Android SDK och iOS SDK mot implementering [Android Chrome, anpassade flikar](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

Den aktuella AdobePass-implementeringen använder plattformsspecifika webbvyer för att tillhandahålla webbmiljön för att visa MVPD-inloggningssidan. De här webbvyerna delar inte autentiseringsuppgiftshantering med plattformswebbläsare och användaren kan därför inte använda ett lösenord som sparats i webbläsaren när ett Adobe Primetime-autentiseringsprogram används. Av säkerhetsskäl håller vissa plattformar dessutom på att bli inaktuella i WebView-styrenheterna för autentiseringsuppgifter. Både Google och Apple har alternativa alternativ som&quot;Anpassade flikar i Chrome&quot; och&quot;Safari View Controller&quot;. De här flikarna är i stort sett enkla att använda i sina respektive webbläsare. Adobe Primetime Authentication antar dessa nya komponenter under 2018.

## Information {#details}

För närvarande finns det två sätt på vilka Adobe Pass Authentication identifierar och registrerar program:

* webbläsarbaserade klienter registreras via tillåten domänlista
* Inbyggda programklienter, som iOS och Android-program, registreras via den signerade beställarens mekanism

Adobe Pass föreslår en ny klientregistreringsmekanism för registrering av nya program för att hantera de nya flödena för Chrome Custom Tabs &amp; Safari View Controller. Den här mekanismen ger en säkrare och mer detaljerad kontroll över dina program och kan användas för att registrera program på alla plattformar.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
