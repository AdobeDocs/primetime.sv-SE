---
seo-title: JSON-objekt för berättiganderesurs-ID
title: JSON-objekt för berättiganderesurs-ID
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: Följande kodblock innehåller ett exempel på ett JSON-objekt när berättiganderesurs-ID:t är en enkel textsträng.
seo-description: Följande kodblock innehåller ett exempel på ett JSON-objekt när berättiganderesurs-ID:t är en enkel textsträng.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

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
