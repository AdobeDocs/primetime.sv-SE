---
description: Om pttrackingmode=simple eller ptplayer=ios-mobileweb skickar manifestservern tillbaka en JSON-formaterad fil som innehåller Överordnad-M3U8, en URL som klienten kan använda för att begära M3U8-filen som beskriver innehållet.
title: JSON-format för URL för begäran om spellista för variantmanifest
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# JSON-format för URL för begäran om spellista för variantmanifest {#json-format-for-url-for-requesting-variant-manifest-playlist}

If `pttrackingmode=simple` eller `ptplayer=ios-mobileweb`, skickar manifestservern tillbaka en JSON-formaterad fil som innehåller Överordnad-M3U8, en URL som klienten kan använda för att begära M3U8-filen som beskriver innehållet.

Det här är formatet på JSON-filen som innehåller `Master-M3U8` URL.

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
