---
description: Du kan ställa in knappar som anropar TVSDK-metoder för att pausa och spela upp media.
seo-description: Du kan ställa in knappar som anropar TVSDK-metoder för att pausa och spela upp media.
seo-title: Implementera en uppspelnings-/pausknapp
title: Implementera en uppspelnings-/pausknapp
uuid: eccdce4b-0114-4389-b5ee-74fe62d38ed8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Implementera en uppspelnings-/pausknapp{#implement-a-play-pause-button}

Du kan ställa in knappar som anropar TVSDK-metoder för att pausa och spela upp media.

Använd följande exempelkod för att implementera en uppspelnings- eller pausknapp:

<!--<a id="example_BC2632D673FE451190A30A23145090D0"></a>-->

```
_playPauseButton =  
[[UIButton alloc] initWithFrame:CGRectMake(BUTTON_POS_X, BUTTON_POS_Y, BUTTON_SIZE_W, BUTTON_SIZE_H)]; 
[_playPauseButton setImage:[UIImage imageNamed:@"play.png"] forState:UIControlStateNormal];  
[_playPauseButton setImage:[UIImage imageNamed:@"pause.png"] forState:UIControlStateSelected]; 
[_playPauseButton addTarget:self action:@selector(playTouch:) forControlEvents:UIControlEventTouchUpInside]; 
[self addSubview:_playPauseButton]; 
 
... 
 
- (void)playTouch:(id)sender { 
    if (self.player.status == PTMediaPlayerStatusPlaying) { 
        _playPauseButton.selected = YES;  
        [self.player pause]; 
    } 
    else { 
        _playPauseButton.selected = NO; [self.player play]; 
    } 
} 
```

