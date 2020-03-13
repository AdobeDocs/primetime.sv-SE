---
description: Om pttrackingmode=simple eller ptplayer=ios-mobileweb skickar manifestservern tillbaka en JSON-formaterad fil som innehåller Master-M3U8, en URL som klienten kan använda för att begära M3U8-filen som beskriver innehållet.
seo-description: Om pttrackingmode=simple eller ptplayer=ios-mobileweb skickar manifestservern tillbaka en JSON-formaterad fil som innehåller Master-M3U8, en URL som klienten kan använda för att begära M3U8-filen som beskriver innehållet.
seo-title: JSON-format för URL för begäran om spellista för variantmanifest
title: JSON-format för URL för begäran om spellista för variantmanifest
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# JSON-format för URL för begäran om spellista för variantmanifest {#json-format-for-url-for-requesting-variant-manifest-playlist}

Om `pttrackingmode=simple` eller `ptplayer=ios-mobileweb`så skickar manifestservern tillbaka en JSON-formaterad fil som innehåller Master-M3U8, en URL som klienten kan använda för att begära M3U8-filen som beskriver innehållet.

Detta är formatet för JSON-filen som innehåller `Master-M3U8` URL:en.

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
