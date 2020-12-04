---
description: 'null'
seo-description: 'null'
seo-title: Ange XSTS-token i spelaren
title: Ange XSTS-token i spelaren
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b
workflow-type: tm+mt
source-wordcount: '66'
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

