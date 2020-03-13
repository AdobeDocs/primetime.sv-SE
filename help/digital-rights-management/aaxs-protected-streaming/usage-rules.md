---
seo-title: Användningsregler
title: Användningsregler
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Användningsregler{#usage-rules}

Med Adobe Access Server for Protected Streaming anges alla användningsregler på servern via konfigurationsfiler. Alla användningsregler som anges i det skyddade innehållet åsidosätts, så vi rekommenderar att du använder en enkel anonym princip under paketeringen av innehållet. Användningsregler som kan konfigureras kan anges per innehavare.

Adobe Access Server for Protected Streaming stöder följande användningsregler:

* Utdataskydd
* Programbegränsningar för Adobe® AIR®, SWF, iOS och Android
* Begränsningar för DRM- och körningsmodulen
* Tillämpning av jailbreak-identifiering (på Adobe Access-plattformar med stöd för jailbreak-identifiering)
* Licenscache är inaktiverat som standard. Licenscache kan aktiveras genom att du anger cachelagringens slutdatum eller så tillåts en viss tid (med början när licensen utfärdas).
* Flera uppspelningsrättigheter, där du kan ange olika kombinationer av utdataskydd, programbegränsningar och DRM/körningsbegränsningar. Du kan till exempel ange olika krav för utdataskydd för varje klientplattform genom att använda DRM-modulbegränsningen med utdataskyddet.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>För att ge stöd för fjärrnyckelleverans till iOS-enheter måste fjärrnyckelleveransen vara aktiverad för den princip som används vid paketeringen. Den här inställningen kan inte ändras via klientkonfigurationen på servern. ***Adobe Primetime krävs för att skapa iOS-applikationer som kan spela upp Adobe Access-skyddat innehåll.***

