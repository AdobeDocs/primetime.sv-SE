---
title: Använda DRMContentData för att ladda licenser i förväg
description: Använda DRMContentData för att ladda licenser i förväg
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Använda DRMContentData för att förhandsladda licenser{#using-drmcontentdata-to-pre-load-licenses}

Följande steg beskriver arbetsflödet för att förhandsladda licensen för en skyddad mediefil med ett `DRMContentData`-objekt.

1. Hämta binära DRM-metadata för det packade innehållet.

   Om du använder referensimplementeraren för Java i Primetime DRM skapas den här metadatafilen automatiskt med tillägget [!DNL .metadata]. Du kan till exempel hämta dessa metadata med klassen `URLLoader`. Om du använder HLS- eller HDS-innehåll refereras metadata till i innehållsmanifestfilen ( [!DNL .m3u8] eller [!DNL .f4m]) eller inkluderas *i* manifestfilen som en Base64-kodad sträng (som måste vara Base64-avkodad före förbrukning).
1. Skapa ett `DRMContentData`-objekt och skicka metadata till konstruktorfunktionen:

   ```
   var drmData:DRMContentData = new DRMContentData( metadata );
   ```

1. Resten av stegen är identiska med arbetsflödet som beskrivs i *Processinformation för skydd av innehåll*.

<!--<a id="example_EBEDA8E10F6344CABA4DE31DC342B8F8"></a>-->

```
import flash.events.DRMAuthenticationCompleteEvent; 
import flash.events.DRMAuthenticationErrorEvent; 
import flash.events.DRMErrorEvent; 
import flash.events.DRMStatusEvent; 
import flash.events.NetStatusEvent; 
import flash.net.NetConnection; 
import flash.net.Primetime; 
import flash.net.PrimetimePlayOptions; 
import flash.net.drm.AuthenticationMethod; 
import flash.net.drm.DRMContentData; 
import flash.net.drm.DRMManager; 
import flash.net.drm.LoadVoucherSetting; 
  
public class DRMPreloader extends Sprite  { 
    private var videoURL:String = "app-storage:/video.flv"; 
    private var userName:String = "user"; 
    private var password:String = "password"; 
    private var preloadConnection:NetConnection; 
    private var preloadStream:Primetime; 
    private var drmManager:DRMManager = DRMManager.getDRMManager(); 
 
    private var drmContentData:DRMContentData; 
 
    public function DRMPreloader():void { 
        drmManager.addEventListener(  
          DRMAuthenticationCompleteEvent.AUTHENTICATION_COMPLETE,  
          onAuthenticationComplete 
        ); 
        drmManager.addEventListener( 
          DRMAuthenticationErrorEvent.AUTHENTICATION_ERROR,  
          onAuthenticationError 
        ); 
        drmManager.addEventListener( 
          DRMStatusEvent.DRM_STATUS, onDRMStatus); 
        drmManager.addEventListener( 
          DRMErrorEvent.DRM_ERROR, onDRMError); 
        preloadConnection = new NetConnection(); 
        preloadConnection.addEventListener( 
          NetStatusEvent.NET_STATUS, onConnect); 
        preloadConnection.connect(null);  
    } 
 
    private function onConnect( event:NetStatusEvent ):void {  
        preloadMetadata(); 
    } 
 
    private function preloadMetadata():void {  
        preloadStream = new Primetime( preloadConnection ); 
        preloadStream.client = this; 
        var options:PrimetimePlayOptions = new PrimetimePlayOptions(); 
        options.streamName = videoURL; 
        preloadStream.preloadEmbeddedData( options );  
    }  
 
    public function onDRMContentData( drmMetadata:DRMContentData ):void {  
        drmContentData = drmMetadata; 
        if ( drmMetadata.authenticationMethod ==  
               AuthenticationMethod.USERNAME_AND_PASSWORD ) {  
            authenticateUser(); 
        } 
        else {  
            getVoucher(); 
        } 
    } 
 
    private function getVoucher():void {  
        drmManager.loadVoucher(  
          drmContentData,  
          LoadVoucherSetting.ALLOW_SERVER  
        ); 
    } 
 
    private function authenticateUser():void {  
        drmManager.authenticate(  
          drmContentData.serverURL,  
          drmContentData.domain,  
          userName,  
          password  
        ); 
    } 
 
    private function onAuthenticationError(  
      event:DRMAuthenticationErrorEvent ):void {  
        trace( "Authentication error: " +  
               event.errorID + ", " +  
               event.subErrorID ); 
    } 
 
    private function onAuthenticationComplete(  
      event:DRMAuthenticationCompleteEvent ):void {  
        trace( "Authenticated to: " +  
               event.serverURL + ",  
               domain: " +  
               event.domain ); 
        getVoucher(); 
    } 
 
    private function onDRMStatus( event:DRMStatusEvent ):void { 
        trace( "DRM Status: " + event.detail); 
        trace("--License allows offline playback = " +  
              event.isAvailableOffline ); 
        trace("--License already cached = " +  
              event.isLocal ); 
        trace("--License required authentication = " +  
              !event.isAnonymous ); 
    } 
 
    private function onDRMError( event:DRMErrorEvent ):void { 
        trace( "DRM error event: " +  
               event.errorID + ", " +  
               event.subErrorID + ", " +  
               event.text ); 
    } 
 
    public function onPlayStatus( info:Object ):void { 
        preloadStream.close(); 
    }  
} 
```

