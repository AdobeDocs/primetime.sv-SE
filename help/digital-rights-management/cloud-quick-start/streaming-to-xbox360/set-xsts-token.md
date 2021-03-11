---
title: Ange XSTS-token i spelaren
description: Ange XSTS-token i spelaren
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Ange XSTS-token i spelaren{#set-the-xsts-token-in-your-player}

I Xbox360 anger du token asynkront som svar på händelsen `MediaPlayer.RequestKeyAttribute`.

Ange XSTS-token.

I exempelappen som medföljer programmet visas hur du ställer in XSTS-token i spelaren. Här är det relevanta kodfragmentet från exempelspelaren:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

