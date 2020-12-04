---
description: 'null'
seo-description: 'null'
seo-title: Konfigurera demoläge för användningsmodell
title: Konfigurera demoläge för användningsmodell
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Konfigurera demoläge för användningsmodell{#configure-usage-model-demo-mode}

Innan referensimplementeringsservern kan utfärda licenser för demonstrationen av användningsmodellen måste du konfigurera servern så att den anger hur licenser genereras för var och en av de fyra användningsmodellerna. Det innebär att du måste ange en DRM-princip för varje användningsmodell. Referensimplementeringen innehåller följande exempel på DRM-principer i katalogen [!DNL Reference Implementation/Server/Reference Implementation Server/resources/]:

* `dto-policy.pol` - (ladda ned till egen enhet)
* `vod-policy.pol` - (Uthyrning/video-on-demand)
* `sub-policy.pol` - (Prenumeration)
* `ad-policy.pol` - (Ad-finansierad)

>[!NOTE]
>
>Du kan ersätta dessa exempelprofiler med dina egna DRM-principer.

1. Ange dessa egenskaper i [!DNL flashaccess-refimpl.properties] för att ange den DRM-princip som du tänker tillämpa på varje användningsmodell:

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. Kopiera dina exempelprincipfiler till den katalog du anger i egenskapen `config.resourcesDirectory` i [!DNL flashaccess-refimpl.properties].
