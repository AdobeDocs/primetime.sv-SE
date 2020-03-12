---
description: Du kan visa den aktuella och återstående tiden för det innehåll som spelas upp.
seo-description: Du kan visa den aktuella och återstående tiden för det innehåll som spelas upp.
seo-title: Visa ett söknavigeringsfält med aktuell position för uppspelningstid
title: Visa ett söknavigeringsfält med aktuell position för uppspelningstid
uuid: db57eb6f-3c67-4a64-a0f4-7e39027eb3e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Visa ett söknavigeringsfält med aktuell position för uppspelningstid {#display-a-seek-scrub-bar-with-the-current-playback-time-position}

Du kan visa den aktuella och återstående tiden för det innehåll som spelas upp.

Använd följande exempelkod för att implementera en rensningslist:

```
// 1. Register for the PTMediaPlayerTimeChangeNotification 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
  name:PTMediaPlayerTimeChangeNotification object:self.player]; 
 
... 
 
_positionSlider = [[UISlider alloc] initWithFrame:CGRectMake(105.0, 14.0, 370, 24)];  
[_positionSlider addTarget:self action:@selector(sliderThumbReleased:)  
  forControlEvents:UIControlEventTouchUpInside]; 
 
... 
 
// 2. Cover the event where the user moves to a different location in the stream 
- (void)sliderThumbReleased:(id)sender { 
    double  sliderTime = [_positionSlider  value];  
    CMTimeRange seekableRange = self.player.seekableRange; 
    if (CMTIMERANGE_IS_VALID(seekableRange)) { 
        double start = CMTimeGetSeconds(seekableRange.start);  
        double duration = CMTimeGetSeconds(seekableRange.duration); 
 
        CMTime newTime = CMTimeMakeWithSeconds((sliderTime * duration) + start, AD_TIMESCALE);  
        [self.player seekToTime:newTime]; 
    } 
} 
 
... 
 
// 3. This method is called whenever the player time changes  
(PTMediaPlayerTimeChangeNotification) 
- (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
    CMTimeRange seekableRange = self.player.seekableRange; 
 
    if (CMTIMERANGE_IS_VALID(seekableRange)) { 
        double start = CMTimeGetSeconds(seekableRange.start);  
        double duration = CMTimeGetSeconds(seekableRange.duration); 
        double currentTime = CMTimeGetSeconds(self.player.currentItem.currentTime); 
 
        if (duration > 0) { 
            //Set the position slider value on the current playback time  
            [_positionSlider setValue:((currentTime - start) / duration)]; 
        } 
    } 
} 
```
