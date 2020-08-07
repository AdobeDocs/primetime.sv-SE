---
description: Med Adobe Primetime DRM Server for Protected Streaming kan du ange alla användningsregler på servern med konfigurationsfiler.
seo-description: Med Adobe Primetime DRM Server for Protected Streaming kan du ange alla användningsregler på servern med konfigurationsfiler.
seo-title: Om användningsregler
title: Om användningsregler
uuid: 4a794712-db58-43f5-b867-8871e58e12ae
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Om användningsregler{#about-usage-rules}

Med Adobe Primetime DRM Server for Protected Streaming kan du ange alla användningsregler på servern med konfigurationsfiler.

Alla användningsregler som anges i DRM-principen för det skyddade innehållet åsidosätts. Därför rekommenderar Adobe att du använder en enkel, anonym DRM-princip när innehåll paketeras. Alla användningsregler som du kan konfigurera kan konfigureras per klientorganisation.

DRM-servern Primetime för skyddad direktuppspelning stöder följande användningsregler:

* Utdataskydd
* Programbegränsningar för Adobe® AIR®, SWF, iOS och Android
* Begränsningar för DRM- och körningsmodulen
* Krävande av jailbreak-identifiering på Primetimes DRM-plattformar som stöder jailbreak-identifiering
* Licenscache är inaktiverat som standard. Licenscachning som du kan aktivera genom att ange cachelagringsslutdatum eller hur lång tid cachning tillåts; börjar när licensen utfärdas.
* Flera uppspelningsrättigheter som gör att du kan ange olika kombinationer av utdataskydd, programbegränsningar och DRM/körningsbegränsningar. Du kan till exempel ange olika krav för utdataskydd för varje klientplattform genom att använda DRM-modulbegränsningen med utdataskyddet.

>[!NOTE]
>
>Om du vill ha stöd för fjärrnyckelleverans till iOS-enheter måste fjärrnyckelleveransen vara aktiverad för den DRM-princip som tillämpas vid paketeringen. Den här inställningen kan inte ändras via klientkonfigurationen på servern.

