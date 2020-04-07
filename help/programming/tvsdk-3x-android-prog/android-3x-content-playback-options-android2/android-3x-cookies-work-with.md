---
description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
seo-description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
seo-title: Arbeta med cookies
title: Arbeta med cookies
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: 5ada8632a7a5e3cb5d795dc42110844244656095

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

1. Skapa en `cookieManager` och lägg till dina cookies för URI:er i din cookieStore.

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

   TVSDK frågar detta `cookieManager` under körning, kontrollerar om det finns några cookies som är associerade med URL:en och använder automatiskt dessa cookies.

   Om cookies måste uppdateras i programmet under uppspelning ska du inte använda `networkConfiguration.setCookieHeaders` API eftersom uppdateringen sker i JAVA-cookie-butiken.

   `networkConfiguration.setCookieHeaders` API ställer in cookies till TVSDK&#39;s C++ CookieStore.

   När du använder JAVA-cookies och delar dem mellan Application och TVSDK använder du JAVA CookieStore för att hantera endast cookies.

   Innan uppspelningen initieras anger du cookies till CookieStore med Cookie Manager enligt ovan.

   Den cookie som lagras i CookieStore hämtas automatiskt av TVSDK.

   Om ett cookie-värde behöver uppdateras senare under uppspelningen anropar du samma tilläggsmetod för CookieStore med samma nyckel och ett nytt värdefält.

   Även angiven
   `networkConfiguration.setReadSetCookieHeader`(false) före anrop
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >När du har angett värdet false för setReadSetCookieHeader anger du cookies för nyckelbegäranden med hjälp av JAVA cookie-hanteraren.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Det här återanrops-API:t aktiveras när det finns en uppdatering i C++-cookies (cookies som kommer från http-svar). Programmet behöver lyssna på det här återanropet och kan uppdatera JAVA CookieStore så att deras nätverksanrop i JAVA kan använda cookies enligt nedan:

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
