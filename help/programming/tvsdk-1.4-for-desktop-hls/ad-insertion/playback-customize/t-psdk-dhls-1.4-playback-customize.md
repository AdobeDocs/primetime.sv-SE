---
description: Du kan anpassa eller åsidosätta annonsbeteenden.
title: Konfigurera anpassad uppspelning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Konfigurera anpassad uppspelning{#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du kan anpassa eller åsidosätta annonsbeteenden måste du registrera annonsprincipinstansen med .
Gör något av följande om du vill anpassa annonsbeteenden:

* Implementera `AdPolicySelector` -gränssnittet och alla dess metoder.

  Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteenden för annonser.

* Utöka `DefaultAdPolicySelector` och bara implementera beteenden som kräver anpassning.

  Det här alternativet rekommenderas om du bara behöver åsidosätta **några** standardbeteenden.

Utför följande uppgifter för båda alternativen:

1. Implementera en egen anpassad annonsprincipväljare.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Utöka innehållsfabriken för att använda den anpassade annonsprincipväljaren.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. Registrera den nya innehållsfabriken som ska användas av TVSDK i annonsarbetsflödet.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Om den anpassade innehållsfabriken har registrerats för en specifik ström via `MediaPlayerItemConfig` -klassen rensas den när `MediaPlayer` -instansen har avallokerats. Programmet måste registrera det varje gång en ny uppspelningssession skapas.
