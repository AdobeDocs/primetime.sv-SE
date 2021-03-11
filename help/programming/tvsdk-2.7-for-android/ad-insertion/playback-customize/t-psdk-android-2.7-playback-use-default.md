---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

1. Gör något av följande om du vill använda standardbeteenden:

   * Om du implementerar en egen `AdvertisingFactory`-klass returnerar du null för `createAdPolicySelector`.

   * Om du inte har någon anpassad implementering för klassen `AdvertisingFactory` använder TVSDK en standardväljare för annonspolicy.

## Konfigurera anpassad uppspelning {#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du anpassar eller åsidosätter annonsbeteenden ska du registrera annonspolicyinstansen med TVSDK.

* Implementera gränssnittet `AdPolicySelector` och alla dess metoder.

   Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteendena för annonser.

* Utöka klassen `DefaultAdPolicySelector` och tillhandahåll implementeringar för endast de beteenden som kräver anpassning.

   Det här alternativet rekommenderas om du bara behöver åsidosätta **vissa** av standardbeteendena.

Så här anpassar du annonsbeteenden:

1. Implementera gränssnittet `AdPolicySelector` och alla dess metoder.
1. Tilldela principinstansen som ska användas av TVSDK via reklamfabriken.

   >[!NOTE]
   >
   >Anpassade annonsprinciper som registreras i början av uppspelningen rensas när `MediaPlayer`-instansen avallokeras. Programmet måste registrera en principväljarinstans varje gång en ny uppspelningssession skapas.

   Exempel:

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. Implementera dina anpassningar.