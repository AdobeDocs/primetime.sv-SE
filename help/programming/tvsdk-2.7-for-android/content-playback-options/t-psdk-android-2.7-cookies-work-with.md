---
description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
title: Arbeta med cookies
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Arbeta med cookies {#work-with-cookies}

Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.

Här följer ett exempel på en begäran till nyckelservern med viss autentisering:

1. Kunden loggar in på din webbplats i en webbläsare och deras inloggning visar att kunden får visa innehållet.
1. Baserat på vad licensservern förväntar sig genererar ditt program en autentiseringstoken.

   Det här värdet skickas till TVSDK.
1. TVSDK anger det här värdet i cookie-huvudet.
1. När TVSDK skickar en begäran till nyckelservern om att hämta en nyckel för att dekryptera innehållet, innehåller begäran autentiseringsvärdet i cookie-huvudet.

   Nyckelservern vet att begäran är giltig.

Så här arbetar du med cookies:

Skapa en `cookieManager` och lägg till dina cookies för URI:erna i din cookieStore.

Exempel:

```java
CookieManager cookieManager=new CookieManager(); 
CookieHandler.setDefault(cookieManager);  
HttpCookie cookie=new HttpCookie("lang","fr"); 
cookie.setDomain("twitter.com");  
cookie.setPath("/"); 
cookie.setVersion(0); 
cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
```

>[!TIP]
>
>När 302-omdirigering är aktiverat kan annonsbegäran omdirigeras till en annan domän än den domän som cookien tillhör.

TVSDK skickar frågor till denna `cookieManager` vid körning, kontrollerar om det finns några cookies som är associerade med URL:en och använder automatiskt dessa cookies.

Händelsen MediaPlayerEvent.COOKIES_UPDATED anropas när C++-cookies uppdateras. Denna cookiesUpdatedEvent har en metod, getCookieString(), som returnerar ett strängvärde för cookien.

Ett exempelkodfragment visas nedan:

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```

