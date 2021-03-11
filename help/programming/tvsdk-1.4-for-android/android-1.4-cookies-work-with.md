---
description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
title: Arbeta med cookies
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Arbeta med cookies{#work-with-cookies}

Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.

Här följer ett exempel med någon typ av autentisering när begäranden görs till nyckelservern:

1. Kunden loggar in på er webbplats i en webbläsare och deras inloggning visar att de får visa innehållet.
1. Ditt program genererar en autentiseringstoken baserat på vad licensservern förväntar sig. Skicka värdet till TVSDK.
1. TVSDK anger det värdet i cookie-huvudet.
1. När TVSDK skickar en begäran till nyckelservern om att hämta en nyckel för att dekryptera innehållet, innehåller den begäran autentiseringsvärdet i cookie-huvudet, så nyckelservern vet att begäran är giltig.

Så här arbetar du med cookies:

1. Skapa en `cookieManager` och lägg till dina cookies för URI:erna i din `cookieStore`.

   Exempel:

   >[!IMPORTANT]
   >
   >När 302-omdirigering är aktiverat kan annonsbegäran omdirigeras till en annan domän än den domän som cookien tillhör.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK skickar frågor till denna cookieManager vid körning, kontrollerar om det finns några cookies som är associerade med URL:en och använder dem automatiskt.

   Ett annat alternativ är att använda `cookieHeaders` i `NetworkConfiguration` för att ange en godtycklig cookie-huvudsträng som ska användas för begäranden. Denna cookie-rubrik skickas som standard endast med nyckelbegäranden. Om du vill skicka cookie-huvudet med alla begäranden använder du metoden `NetworkConfiguration` `setUseCookieHeadersForAllRequests`:

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
