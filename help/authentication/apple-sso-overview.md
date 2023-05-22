---
title: Apple SSO - översikt
description: Apple SSO - översikt
exl-id: 7cf47d01-a35a-4c85-b562-e5ebb6945693
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---

# Apple SSO - översikt {#apple-sso-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#Introduction}

Apple tillhandahåller ett API som gör att man kan logga in på sitt TV-leverantörskonto på enhetssystemnivå, vilket eliminerar behovet av att autentisera appvis.

Apple och Adobe Primetime Authentication samarbetade därför för att skapa plattformen Single Sign-On (SSO) för användare i TV Everywhere-ekosystemet för iPhone-, iPad- och Apple TV-ägare.

För att kunna dra nytta av SSO-användarupplevelsen (Single Sign-On) på en Apple-enhet finns det en lista över krav som måste uppfyllas.

</br>

## Förutsättningar {#Prerequisites}

Förutsättningen kan gälla för en eller flera enheter som deltar i TVE-verksamheten, t.ex. programmerare, distributörer av videoprogrammeringstjänster, Adobe Primetime-autentisering eller Apple.

</br>

### Programmer {#Programmer}

För att kunna dra nytta av SSO-användarupplevelsen (Single Sign-On) måste en programmerare:

1. Använd minst Xcode version 8 och iOS/tvOS version 10.

1. Har [Enkel inloggning för videoprenumerant](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) konfigurerat till deras Apple Developer Account. Kontakta Apple för att aktivera [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) för ditt Apple Team ID.

1. Aktivera enkel inloggning (YES) för varje önskad integrering (Channel x MVPD) och önskad plattform (iOS/tvOS) via [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/).

1. Integrera Apple SSO-arbetsflöden med någon av följande två lösningar från Adobe Primetime Authentication Team:

   - Adobe Primetime Authentication REST API har stöd för plattformsautentisering med enkel inloggning (SSO) för slutanvändare av klientprogram som körs på iOS, iPadOS eller tvOS. Se även [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK har stöd för plattformsautentisering med enkel inloggning (SSO) för slutanvändare av klientprogram som körs på iOS, iPadOS eller tvOS. Se även [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>Pro Tip:</u>** För att få tillgång till användarens prenumerationsinformation måste användaren ge programmet behörighet att fortsätta, på samma sätt som att ge åtkomst till enhetens kamera eller mikrofon. Den här behörigheten måste begäras per program och enheten kommer att spara användarens val. Tänk på att användaren kan ändra sitt beslut genom att gå till programinställningarna (behörighet för tv-leverantör) eller till avsnittet från *`Settings -> TV Provider`* på iOS/iPadOS eller *`Settings -> Accounts -> TV Provider`* på tvOS.

   - **<u>Pro Tip:</u>** Vi rekommenderar att du begär användarens tillstånd när programmet försätts i förgrundstillstånd, men det är bara ett förslag eftersom programmet kan söka efter [behörighet att komma åt](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) användarens prenumerationsinformation när som helst innan användarautentisering krävs. Dessutom kommer API:erna för AccessEnabler iOS/tvOS SDK automatiskt att begära användarens tillstånd när användaren behöver det.

   - **<u>Pro Tip:</u>** Vi rekommenderar att man uppmuntrar användare som vägrar ge tillstånd att få tillgång till prenumerationsinformation genom att förklara fördelarna med SSO (Single Sign-On). Tänk på att användaren kan ändra sitt beslut genom att gå till programinställningarna (behörighet för tv-leverantör) eller till avsnittet från *`Settings -> TV Provider`* på iOS/iPadOS eller *`Settings -> Accounts -> TV Provider`* på tvOS.

Resultatet bör ge en upplevelse som överensstämmer med följande användarflöden, som vi rekommenderar att du tittar på innan du börjar utveckla dina program:

- [iPhone/iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) användarflöden
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) användarflöden


>[!IMPORTANT]
>
> När funktionen för enkel inloggning är **aktiverad** för iOS/tvOS **och** i fallet Apple **ombord (stöds) eller väljare** MVPD-dokument för autentiserings-/utloggningsflödena från Apple SSO-arbetsflöden omfattar både Apple- och Adobe Primetime-autentiseringslösningar, medan alla andra flöden (auktorisering, förauktorisering, metadata osv.) kommer endast att hanteras av Adobe Primetime Authentication.


>[!IMPORTANT]
>
> När funktionen för enkel inloggning är **inaktiverad** för iOS/tvOS **eller** i fallet Apple **inte ombord (stöds inte)** MVPD-program kommer autentiserings-/utloggningsflödena att gå tillbaka från Apple SSO-arbetsflöden till de vanliga som hanteras enbart av Adobe Primetime Authentication.


>[!IMPORTANT]
>
> En stor fördel med Apple SSO-arbetsflöde är användarflödet för autentisering på en skärm, som också kan levereras på Apple TV när funktionen för enkel inloggning är **aktiverad** för tvOS **och** i fallet Apple **onboarding (stöds)** MVPD.


### MVPD {#MVPD}

För att kunna dra nytta av SSO-användarupplevelsen (Single Sign-On) måste ett enda MVPD:

 

1. Bli medlem i arbetsflödet för Apple SSO på Apple. Kontakta Apple för att underlätta introduktionsprocessen.
1. Tillhandahåll ett JavaScript TVML-program som kan hantera användarens inloggningsformulär. Kontakta Apple för att få rätt dokumentation.
1. Ange ett strängvärde som representerar den provider-ID som tilldelats av Apple under introduktionsprocessen. Kontakta Adobe Primetime-autentiseringen för att utföra konfigurationsändringar.

</br>

## Vanliga frågor {#FAQ}

1. Om något går fel i Apple SSO-arbetsflöde, kan programmet som använder AccessEnabler iOS/tvOS SDK återgå till det reguljära autentiseringsflödet?
   - Detta är möjligt men kräver att en konfigurationsändring utförs på [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/). The *Aktivera enkel inloggning* måste anges på *NEJ* för den önskade integrationen (Channel x MVPD) och den önskade plattformen (iOS/tvOS).
   - Programmet bekräftar bara konfigurationsändringen efter att ha anropat [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API om det använder AccessEnabler iOS/tvOS SDK.
1. Vet programmet när en autentisering har skett till följd av en inloggning via plattformens SSO på en annan enhet eller ett annat program?
   - Den här informationen kommer inte att vara tillgänglig.
1. Vet programmet när en autentisering har skett som ett resultat av en inloggning via plattformens SSO på samma enhet? 
   - Den här informationen är tillgänglig som en del av användarens metadatanyckel: *tokenSource* som ska returnera strängvärdet: &quot;Apple&quot; i det här fallet.
1. Vad händer om en användare loggar in genom att gå till *`Settings -> TV Provider`* på iOS/iPadOS eller *`Settings -> Accounts -> TV Provider`* på tvOS-avsnitt med ett MVPD som inte är integrerat med programmet?
   - När användaren startar programmet autentiseras inte användaren via arbetsflödet för enkel inloggning i Apple. Därför måste programmet återgå till det reguljära autentiseringsflödet och presentera en egen MVPD-väljare.
1. Vad händer om en användare loggar in genom att gå till *`Settings -> TV Provider`* på iOS/iPadOS eller *`Settings -> Accounts -> TV Provider`* på tvOS-avsnitt med en MVPD som har *Aktivera enkel inloggning* set på *NEJ* på [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/) för iOS/tvOS-plattformen?
   - När användaren startar programmet autentiseras inte användaren via arbetsflödet för enkel inloggning i Apple. Därför måste programmet återgå till det reguljära autentiseringsflödet och presentera en egen MVPD-väljare.
1. Vad händer om en användare har ett MVPD-program som inte har introducerats (stöds inte) av Apple, men som finns i Apple-väljaren?
   - När användaren startar programmet väljer användaren bara MVPD via Apple SSO-arbetsflöde utan att slutföra autentiseringsflödet. Därför måste programmet återgå till det reguljära autentiseringsflödet, men kan använda det redan valda MVPD.
1. Vad händer om en användare har ett MVPD som inte har anammats (stöds inte) av Apple?
   - När användaren startar programmet väljer användaren alternativet &quot;Andra TV-leverantörer&quot; via arbetsflödet för enkel inloggning i Apple. Därför måste programmet återgå till det reguljära autentiseringsflödet och presentera en egen MVPD-väljare.
1. Vad händer om en användare har ett MVPD som bryts ned genom [Adobe Primetime TVE Dashboard](https://console.auth.adobe.com/)?
   - När användaren startar programmet autentiseras användaren via nedbrytningsmekanismen och inte via Apple SSO-arbetsflöde.
   - Upplevelsen bör vara smidig för användaren, medan programmet informeras via *N010* om koden används i AccessEnabler iOS/tvOS SDK.
1. Kommer MVPD-användar-ID att ändras mellan Apple SSO och SSO-autentiseringsflödet utanför Apple?
   - Förväntningen är att användar-ID inte ändras, men måste verifieras för varje vald leverantör. 
1. Kommer autentiserings-TTL att ändras?
   - Adobe Primetime Authentication fortsätter att respektera de TTL:er som krävs av programmerarna för deras integrering med varje MVPD.
   - När du navigerar från ett programmeringsprogram till ett annat programmeringsprogram via Apple SSO, kommer det andra programmet att ha en TTL för motsvarande programmeringsprogram x MVPD-integrering (det delar inte TTL-värdet för det första programmet som autentiseras)

|  | Adobe Primetime-autentiserings-TTL har gått ut | Adobe Primetime Authentication TTL valid |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple enhetstoken TTL har gått ut** | användaren är INTE autentiserad (MVPD-väljaren ska visas) | användaren är autentiserad och TTL är den återstående tiden för denna Adobe Primetime Authentication-token |
| **Apple enhetstoken TTL är giltig** | användaren är tyst autentiserad och hämtar en annan Adobe Primetime-autentiseringstoken med den TTL som anges i TVE Dashboard | användaren är autentiserad och TTL är den återstående tiden för denna Adobe Primetime Authentication-token |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
