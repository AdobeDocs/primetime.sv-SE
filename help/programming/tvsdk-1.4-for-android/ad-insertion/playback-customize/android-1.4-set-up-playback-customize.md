---
description: Du kan anpassa eller åsidosätta annonsbeteenden.
title: Konfigurera anpassad uppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 1%

---


# Konfigurera anpassad uppspelning {#cset-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteendet genom att registrera annonsprincipinstansen med TVSDK.

Gör något av följande om du vill anpassa annonsbeteenden:

* Implementera gränssnittet `AdPolicySelector` och alla dess metoder.
Det här alternativet rekommenderas om du behöver åsidosätta alla standardbeteenden för annonser.

* Utöka klassen `DefaultAdPolicySelector` och endast tillhandahålla implementeringar för de beteenden som kräver
anpassning.
Det här alternativet rekommenderas om du bara behöver åsidosätta några av standardbeteendena.

Utför följande uppgifter för båda alternativen:

Så här anpassar du annonsbeteenden:

1. Implementera gränssnittet AdPolicySelector och alla dess metoder.

1. Tilldela principinstansen som ska användas av TVSDK via reklamfabriken.

>[!IMPORTANT]
>
>Anpassade annonsprinciper som registreras i början av >uppspelning rensas när MediaPlayer-instansen >avallokeras. Programmet måste registrera en princip >väljarinstansen varje gång en ny uppspelningssession skapas.

Exempel:

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. Implementera dina anpassningar.