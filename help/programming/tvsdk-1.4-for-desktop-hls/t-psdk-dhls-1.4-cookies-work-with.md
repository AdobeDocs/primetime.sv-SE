---
description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
seo-description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
seo-title: Arbeta med cookies
title: Arbeta med cookies
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Arbeta med cookies{#work-with-cookies}

Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.

Här följer ett exempel med någon typ av autentisering när begäranden görs till nyckelservern:

1. Kunden loggar in på er webbplats i en webbläsare och deras inloggning visar att de får visa innehållet.
1. Ditt program genererar en autentiseringstoken baserat på vad licensservern förväntar sig. Skicka värdet till TVSDK.
1. TVSDK anger det värdet i cookie-huvudet.
1. När TVSDK skickar en begäran till nyckelservern om att hämta en nyckel för att dekryptera innehållet, innehåller den begäran autentiseringsvärdet i cookie-huvudet, så nyckelservern vet att begäran är giltig.

Så här arbetar du med cookies:

1. Använd egenskapen `cookieHeaders` i `NetworkConfiguration` för att ange en cookie. Egenskapen är ett Metadata-objekt och du kan lägga till nyckelvärdepar till det här objektet som ska inkluderas i cookie-huvudet. `cookieHeaders`

   Exempel:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Som standard skickas endast cookie-huvuden med nyckelförfrågningar. Om du vill skicka cookie-huvuden med alla förfrågningar ställer du in egenskapen på `NetworkConfiguration` true `useCookieHeadersForAllRequests` .

1. Om du vill vara säker på att det `NetworkConfiguration` fungerar anger du det som metadata:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Ange metadata från föregående steg när du skapar en `MediaResource`.

   Om du till exempel använder `createFromURL` metoden anger du följande information:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

