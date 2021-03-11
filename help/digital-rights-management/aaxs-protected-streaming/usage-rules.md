---
title: Användningsregler
description: Användningsregler
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Användningsregler{#usage-rules}

Med Adobe Access Server för skyddad strömning anges alla användningsregler på servern via konfigurationsfiler. Alla användningsregler som anges i det skyddade innehållet åsidosätts, så vi rekommenderar att du använder en enkel anonym princip under paketeringen av innehållet. Användningsregler som kan konfigureras kan anges per innehavare.

Adobe Access Server för skyddad strömning stöder följande användningsregler:

* Utdataskydd
* Programbegränsningar för Adobe® AIR®, SWF, iOS och Android
* Begränsningar för DRM- och körningsmodulen
* Tillämpning av jailbreak-identifiering (på Adobe Access-plattformar med stöd för jailbreak-identifiering)
* Licenscache är inaktiverat som standard. Licenscache kan aktiveras genom att du anger cachelagringens slutdatum eller så tillåts en viss tid (med början när licensen utfärdas).
* Flera uppspelningsrättigheter, där du kan ange olika kombinationer av utdataskydd, programbegränsningar och DRM/körningsbegränsningar. Du kan till exempel ange olika krav för utdataskydd för varje klientplattform genom att använda DRM-modulbegränsningen med utdataskyddet.

>[!NOTE]
>
>För att ge stöd för fjärrnyckelleverans till iOS-enheter måste fjärrnyckelleveransen vara aktiverad för den princip som används vid paketeringen. Den här inställningen kan inte ändras via klientkonfigurationen på servern. ***Adobe Primetime krävs för att skapa iOS-program som kan spela upp Adobe Access-skyddat innehåll.***

