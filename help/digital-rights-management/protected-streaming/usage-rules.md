---
description: Med Adobe Primetime DRM Server for Protected Streaming kan du ange alla användningsregler på servern med konfigurationsfiler.
title: Om användningsregler
exl-id: 55af3a18-8fdb-4285-bd9f-ca479475e34f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '240'
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
>Om du vill ha stöd för fjärrnyckelleverans till iOS-enheter måste fjärrnyckelleveransen vara aktiverad för DRM-principen som tillämpas vid paketeringstiden. Den här inställningen kan inte ändras via klientkonfigurationen på servern.
