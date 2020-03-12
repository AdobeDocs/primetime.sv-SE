---
description: Begäran om berättigande och svar skickas via en ömsesidigt autentiserad SSL-anslutning mellan licensservern och kundens tillståndstjänst.
seo-description: Begäran om berättigande och svar skickas via en ömsesidigt autentiserad SSL-anslutning mellan licensservern och kundens tillståndstjänst.
seo-title: SE Offentligt API
title: SE Offentligt API
uuid: f3a17d61-04ee-4bdb-9d64-a98066c6d1c8
translation-type: tm+mt
source-git-commit: 15403abbd53486e1faa2146cda83f41bd8116632

---


# SE Offentligt API {#sees-public-api}

Begäran om berättigande och svar skickas via en ömsesidigt autentiserad SSL-anslutning mellan licensservern och kundens tillståndstjänst.

HTTPS-URI-schemat ( [https://tools.ietf.org/html/rfc7230#section-2.7.2](https://tools.ietf.org/html/rfc7230#section-2.7.2)) används för att definiera tillståndsslutpunkten, och HTTP POST-förfrågningsmetoden ( [https://tools.ietf.org/html/rfc7231#section-4.3.3](https://tools.ietf.org/html/rfc7231#section-4.3.3)) används för begäran. Slutpunkten för berättigandet, samt en flagga som anger serverdelsberättigandet, krävs och måste ingå i policyn vid paketeringstiden.

## Berättigandebegäran {#section_BFBFEF0795CA46D6842C479256B95F95}

Innehållet i berättigandebegäran blir ett JSON-objekt som definieras enligt nedan.

**Objektdefinition för JSON-tillståndsbegäran**

```
{ 
 "title" : "Entitlement Request", 
 "type" : "object", 
 "properties" : { 
  "messageID" : { 
   "type" : "string", 
   "description" : "Unique ID for this message (GUID).  Used to confirm that the subsequent response is actually for this request." 
  }, 
  "version" : { 
   "type" : "integer", 
   "description" : "Version number of the protocol, currently 1." 
  }, 
  "requestType" : { 
   "type" : "integer", 
   "description" : "Request type. 1 - time based entitlement request, 2 - device registration entitlement request 3 - device bound entitlement request." 
  }, 
  "contentID" : { 
   "type" : "string", 
   "description" : "Content ID (GUID) that was given to the content during packaging time." 
  }, 
  "customerCookie" : { 
   "type" : "string", 
   "description" : "Customer cookie. Cookie is just arbitrary string up to 32 characters long." 
  } 
    }, 
 "required" : ["messageID", "version", "contentID"] 
}
```

## Tillståndssvar {#section_F15A9FD6BAD946B3B4C5C14612F90154}

Innehållet i tillståndssvaret är ett JSON-objekt.

**Definition av JSON-berättigandesvarsobjekt**

```
{ 
  "title" : "Entitlement Response", 
  "type" : "object", 
  "properties" : { 
    "messageID" : { 
    "type" : "string", 
    "description" : "Unique ID from the Entitlement Request message.   
      Must match, or entitlement will be denied." 
  }, 
  "version" : { 
    "type" : "integer", 
    "description" : "Version number of the protocol; must be <= the version number  
      from the Entitlement Request message." 
  }, 
  "isAllowed" : { 
    "type" : "boolean", 
    "description" : "Grant the license or not." 
  }, 
  "epTokenURL" : { 
    "type" : "string", 
    "description" : "ExpressPlay Token URL" 
  }, 
  "error" : { 
    "type" : "integer", 
    "description" : "An error number produced by the entitlement server.  
      Will be passed to the client as the 'code' field of the server error response." 
  }, 
  "errorText" : { 
    "type" : "string", 
    "description" : "Additional error information produced by the entitlement server.  
      Will be passed to the client as the 'text' field of the server error response." 
  }, 
  "required" : ["messageID", "version", "isAllowed", "epTokenURL"] 
}
```
