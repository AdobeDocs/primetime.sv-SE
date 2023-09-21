---
description: PTMediaPlayer-gränssnittet kapslar in funktionaliteten och beteendet i ett mediespelarobjekt.
title: Konfigurera PTMediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Konfigurera PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK innehåller verktyg för att skapa ett avancerat videospelarprogram (din Primetime-spelare) som du kan integrera med andra Primetime-komponenter.

Använd plattformens verktyg för att skapa en spelare och ansluta den till mediespelarvyn i TVSDK, som har metoder för att spela upp och hantera videoklipp. TVSDK innehåller till exempel metoderna play och pause. Du kan skapa knappar för användargränssnitt på din plattform och ställa in knapparna för att anropa dessa TVSDK-metoder.

PTMediaPlayer-gränssnittet kapslar in funktionaliteten och beteendet i ett mediespelarobjekt.

För att konfigurera `PTMediaPlayer`:

1. Hämta mediets URL från användargränssnittet, till exempel, i ett textfält.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Skapa `PTMetadata`.

   Anta att din metod `createMetada` förbereder metadata (se [Reklam](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Skapa `PTMediaPlayerItem` genom att använda `PTMetadata` -instans.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Lägg till observatörer i meddelanden som TVSDK skickar.

   ```
   [self addObservers]
   ```

1. Skapa `PTMediaPlayer` med dina nya `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Ange egenskaper för spelaren.

   Här är några av de tillgängliga `PTMediaPlayer` egenskaper:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Ange spelarens visningsegenskap.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Lägg till spelarens vy i den aktuella vyns undervy.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Utlysning `play` för att starta medieuppspelning.

   ```
   [player play];
   ```
