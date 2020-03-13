---
description: Du kan anpassa eller åsidosätta annonsbeteenden.
seo-description: Du kan anpassa eller åsidosätta annonsbeteenden.
seo-title: Konfigurera anpassad uppspelning
title: Konfigurera anpassad uppspelning
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92

---


# Konfigurera anpassad uppspelning{#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du kan anpassa eller åsidosätta annonsbeteenden måste du registrera annonsprincipinstansen med .
Gör något av följande om du vill anpassa annonsbeteenden:

* Implementera `AdPolicySelector` gränssnittet och alla dess metoder.

   Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteenden för annonser.

* Utöka `DefaultAdPolicySelector` klassen och tillhandahålla implementeringar för endast de beteenden som kräver anpassning.

   Det här alternativet rekommenderas om du bara behöver åsidosätta **vissa** av standardbeteendena.

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
   >Om den anpassade innehållsfabriken registrerades för en viss ström via `MediaPlayerItemConfig` klassen rensas den när `MediaPlayer` instansen frigörs. Programmet måste registrera det varje gång en ny uppspelningssession skapas.