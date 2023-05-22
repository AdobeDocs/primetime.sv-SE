---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
exl-id: eb4ce0b4-9dfd-4de8-8cbf-8aba093a5ddd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Använd standardbeteendet för uppspelning  {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

1. Gör något av följande om du vill använda standardbeteenden:

   * Om du implementerar en egen `AdvertisingFactory` klass, returnera null för `createAdPolicySelector`.

   * Om du inte har någon anpassad implementering för `AdvertisingFactory` klassen TVSDK använder en standardväljare för annonsprinciper.

## Konfigurera anpassad uppspelning {#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du anpassar eller åsidosätter annonsbeteenden ska du registrera annonspolicyinstansen med TVSDK.

* Implementera `AdPolicySelector` -gränssnittet och alla dess metoder.

   Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteenden för annonser.

* Utöka `DefaultAdPolicySelector` och bara implementera beteenden som kräver anpassning.

   Det här alternativet rekommenderas om du bara behöver åsidosätta **några** av standardbeteendena.

Så här anpassar du annonsbeteenden:

1. Implementera `AdPolicySelector` -gränssnittet och alla dess metoder.
1. Tilldela principinstansen som ska användas av TVSDK via reklamfabriken.

   >[!NOTE]
   >
   >Anpassade annonsprinciper som registreras i början av uppspelningen rensas när `MediaPlayer` instansen har avallokerats. Programmet måste registrera en principväljarinstans varje gång en ny uppspelningssession skapas.

   Till exempel:

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
