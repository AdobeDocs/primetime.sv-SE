---
title: Konfigurera demoläge för användningsmodell
description: Konfigurera demoläge för användningsmodell
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
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
