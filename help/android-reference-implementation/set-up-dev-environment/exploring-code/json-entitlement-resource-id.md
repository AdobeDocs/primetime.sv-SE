---
title: JSON-objekt för berättiganderesurs-ID
description: Följande kodblock innehåller ett exempel på ett JSON-objekt när berättiganderesurs-ID:t är en enkel textsträng.
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# JSON-objekt för berättiganderesurs-ID {#json-object-for-entitlement-resource-id}

Följande kodblock innehåller ett exempel på ett JSON-objekt när berättiganderesurs-ID:t är en enkel textsträng. I det här fallet är resurs-ID strängen &quot;resource&quot;.

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

Följande kodblock innehåller ett exempel på ett JSON-objekt när berättiganderesurs-ID:t är en HTML-kodad mRSS-sträng.

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

Följande mRSS-sträng används som resurs-ID.

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
