---
description: Du kan anpassa eller åsidosätta annonsbeteenden.
title: Konfigurera anpassad uppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Konfigurera anpassad uppspelning{#set-up-customized-playback}

Du kan anpassa eller åsidosätta annonsbeteenden.

Innan du kan anpassa eller åsidosätta annonsbeteenden måste du registrera annonsprincipinstansen med .
Gör något av följande om du vill anpassa annonsbeteenden:

* Implementera gränssnittet `AdPolicySelector` och alla dess metoder.

   Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteendena för annonser.

* Utöka klassen `DefaultAdPolicySelector` och tillhandahåll implementeringar för endast de beteenden som kräver anpassning.

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
   >Om den anpassade innehållsfabriken registrerades för en specifik ström via klassen `MediaPlayerItemConfig` rensas den när instansen `MediaPlayer` tas bort. Programmet måste registrera det varje gång en ny uppspelningssession skapas.