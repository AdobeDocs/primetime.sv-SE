---
title: Stöd för WKWebView i iOS SDK 3.1+
description: Stöd för WKWebView i iOS SDK 3.1+
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Stöd för WKWebView i iOS SDK 3.1+ {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>

**Eftersom Apple har ersatt UIWebView i iOS har vi uppdaterat iOS SDK 3.1 med stöd för WKWebView.**

## Kompatibilitet {#compatibility}

Från och med iOS SDK version 3.1 kan implementerare nu använda WKWebView eller UIWebView som båda ska användas. Eftersom UIWebView är borttaget av Apple bör appar migreras till WKWebView för att undvika problem med framtida iOS-versioner.

Observera att migrering innebär att du helt enkelt byter UIWebView-klass till WKWebView. Det finns inget specifikt arbete att göra med Adobe AccessEnabler.

## Kända fel {#known-issues}

Adobe AccessEnabler använde en dold intern UIWebView-instans för att utföra[passiv autentisering](/help/authentication/sso-passive-authn.md)&quot; för vissa MVPD. Det&quot;passiva&quot; flödet var användbart för MVPD-program som kräver autentisering för varje begärande-ID, och från det här flödet användes programmerare som använde samma team-ID i flera iOS-program för att simulera en SSO-upplevelse (Adobe SSO). Den här funktionen används för närvarande av ett begränsat antal MVPD-program.

Funktionen använde ett beteende hos UIWebView som gjorde att Adobe kunde hämta autentiseringscookies och spela upp dem igen under det passiva flödet. WKWebView har nu en starkare säkerhet som förhindrar Adobe att hämta cookies som angetts vid inloggning och spela upp dem igen med en dold instans av WKWebView. På grund av den här säkerhetsförbättringen och med tanke på att det passiva flödet endast omfattade en mycket begränsad uppsättning programmeringsdokument i ett mycket specifikt implementeringsscenario (flera program som använder samma team-ID) tog Adobe bort funktionen&quot;passiv autentisering&quot; för programmeringsvideoprogrammeringsprogram som använder webbvyer för autentisering.

Funktionen finns fortfarande för MVPD-program som är konfigurerade att använda SFSafariViewController, men observera att i det här fallet är den &quot;passiva&quot; autentiseringen synlig för användaren eftersom SFSafariViewController inte kan användas på ett &quot;dolt&quot; sätt.
