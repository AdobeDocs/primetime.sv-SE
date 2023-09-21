---
description: Flash Runtime TVSDK behöver en signerad token för att verifiera att du har behörighet att anropa TVSDK API på domänen där ditt program finns.
title: Läs in din signerade token
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Läs in din signerade token {#load-your-signed-token}

Flash Runtime TVSDK behöver en signerad token för att verifiera att du har behörighet att anropa TVSDK API på domänen där ditt program finns.

1. Hämta en signerad token från din Adobe-representant för var och en av dina domäner (där varje domän kan vara en specifik domän eller en jokerteckendomän).

       Om du vill hämta en token anger du Adobe med antingen domänen där ditt program ska lagras eller läsas in, eller, helst, domänen som en SHA256-hash. Adobe tillhandahåller i gengäld en signerad token för varje domän. Dessa variabler har någon av följande former:
   
   * An [!DNL .xml] som fungerar som token för en enda domän eller jokerteckendomän.

     >[!NOTE]
     >
     >En token för en jokerteckendomän täcker den domänen och alla dess underdomäner. En jokertecken för domänen [!DNL mycompany.com] skulle även täcka [!DNL vids.mycompany.com] och [!DNL private.vids.mycompany.com]; en jokertecken-token för [!DNL vids.mycompany.com] skulle även täcka [!DNL private.vids.mycompany.com]. *Jokertecken för domäntoken stöds bara för vissa Flashar Player.*

   * A [!DNL .swf] -fil som innehåller tokeninformation för flera domäner (exklusive jokertecken) (en eller jokertecken) som programmet kan läsa in dynamiskt.

1. Lagra tokenfilen på samma plats eller i samma domän som ditt program.

   Som standard söker TVSDK efter token på den här platsen. Du kan också ange tokens namn och plats i `flash_vars` i filen HTML.
1. Om din tokenfil är en enda XML-fil:
   1. Använd `utils.AuthorizedFeaturesHelper.loadFrom` för att hämta data som lagras på den angivna URL:en (tokenfilen) och extrahera `authorizedFeatures` information från den.

      Det här steget kan variera. Du kanske vill utföra autentiseringen innan du startar programmet, eller så kanske du får token direkt från ditt innehållshanteringssystem (CMS).

   1. TVSDK skickar en `COMPLETED` om inläsningen lyckades eller `FAILED` i annat fall. Vidta lämpliga åtgärder när du upptäcker någon av händelserna.

      Detta måste lyckas för att ditt program ska kunna tillhandahålla de nödvändiga `authorizedFeatures` objekt till TVSDK i form av en `MediaPlayerContext`.

   I det här exemplet visas hur du kan använda en enda token [!DNL .xml] -fil.

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. Om din token är en [!DNL .swf] fil:
   1. Definiera en `Loader` för dynamisk inläsning av [!DNL .swf] -fil.
   1. Ange `LoaderContext` för att ange att inläsningen ska ske i den aktuella programdomänen, vilket gör att TVSDK kan välja rätt token i [!DNL .swf] -fil. If `LoaderContext` har inte angetts, standardåtgärden för `Loader.load` ska läsa in SWF-filen i den underordnade domänen till den aktuella domänen.
   1. Lyssna efter COMPLETE-händelsen som TVSDK skickar om inläsningen lyckas.

      Lyssna också efter FEL-händelsen och vidta lämpliga åtgärder.
   1. Om inläsningen är klar använder du `AuthorizedFeaturesHelper` för att få `ByteArray` som innehåller PCKS-7-kodade säkerhetsdata.

      Dessa data används via AVE V11-API för att få auktoriseringsbekräftelsen från Flash Runtime Player. Om bytearrayen inte har något innehåll använder du proceduren för att söka efter en endomänstokenfil.
   1. Använd `AuthorizedFeatureHelper.loadFeatureFromData` för att hämta data från bytearrayen.
   1. Ta bort [!DNL .swf] -fil.

   I följande exempel visas hur du kan använda en variabel [!DNL .swf] -fil.

   **Exempel på flera token 1:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **Exempel på flera token 2:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```
