---
description: Du kan använda TVSDK för att skicka godtyckliga data i cookie-rubriker för sessionshantering, åtkomst till portar och så vidare.
title: Arbeta med cookies
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '234'
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

1. Använd `cookieHeaders` egenskap i `NetworkConfiguration` för att sätta en kaka. The `cookieHeaders` -egenskapen är ett Metadata-objekt, och du kan lägga till nyckelvärdepar till det här objektet som ska inkluderas i cookie-huvudet.

   Till exempel:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Som standard skickas endast cookie-huvuden med nyckelförfrågningar. Om du vill skicka cookie-huvuden med alla förfrågningar anger du `NetworkConfiguration` property `useCookieHeadersForAllRequests` till true.

1. Se till att `NetworkConfiguration` fungerar, anger det som metadata:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Ange metadata från föregående steg när du skapar en `MediaResource`.

   Om du till exempel använder `createFromURL` anger du följande information:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
