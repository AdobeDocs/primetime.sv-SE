---
description: Manifestservern koordinerar de system som tillhandahåller innehåll, tillhandahåller annonser, spelar upp video och spårar annonser. Den får M3U8-kodade spellistor (manifest) som klientvideospelare tar emot från innehållsleverantörer, knyter ihop annonser från annonsleverantörer i manifesten och skickar de sammanslagna manifesten till videospelare. Det har stöd för både annonsspårning på klientsidan och serversidan. Den utför sina interaktioner med ett HTTP-baserat webbtjänstgränssnitt.
seo-description: Manifestservern koordinerar de system som tillhandahåller innehåll, tillhandahåller annonser, spelar upp video och spårar annonser. Den får M3U8-kodade spellistor (manifest) som klientvideospelare tar emot från innehållsleverantörer, knyter ihop annonser från annonsleverantörer i manifesten och skickar de sammanslagna manifesten till videospelare. Det har stöd för både annonsspårning på klientsidan och serversidan. Den utför sina interaktioner med ett HTTP-baserat webbtjänstgränssnitt.
seo-title: Översikt över Manifest Server-interaktioner
title: Översikt över Manifest Server-interaktioner
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Översikt över Manifest Server-interaktioner {#overview-of-manifest-server-interactions}

Manifestservern koordinerar de system som tillhandahåller innehåll, tillhandahåller annonser, spelar upp video och spårar annonser. Den får M3U8-kodade spellistor (manifest) som klientvideospelare tar emot från innehållsleverantörer, knyter ihop annonser från annonsleverantörer i manifesten och skickar de sammanslagna manifesten till videospelare. Det har stöd för både annonsspårning på klientsidan och serversidan. Den utför sina interaktioner med ett HTTP-baserat webbtjänstgränssnitt.

En typisk konfiguration innehåller:

* Primetimes manifestserver
* Primetime Creative Repackaging Service (CRS)
* En klient, styra en videospelare
* En utgivare, vanligtvis med ett CMS-system (Content Management System)
* Ett CDN (Content Delivery Network)
* En annonsserver
* En mottagare för annonsspårningsrapporter

Arbetsflödet varierar beroende på ett antal faktorer, till exempel om CDN är Akamai eller om klienten utför annonsspårning. Ett diagram över arbetsflödet för annonsspårning på klientsidan finns i [Arbetsflöde för spårning på klientsidan](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

Manifestservern interagerar med videoutsändningsklienter genom att ta emot och besvara HTTP GET-begäranden. Svaren är M3U8-kodade manifest som beskriver reklamsyrat innehåll, eventuellt inklusive en JSON- eller VMAP-struktur (sidecar) som innehåller detaljerade anvisningar för annonsspårning (se [Filformat](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Ett typiskt arbetsflöde ser ut så här:

1. Utgivaren skickar innehålls-URL:en och information för annonsservern till klienten.
1. Klienten använder informationen från utgivaren för att generera en URL för en manifestserver och skickar en GET-begäran till den URL:en. Detta kallas Bootstrap URL.
1. Manifestservern upprättar en session med klienten.
1. Manifestservern hämtar innehållsmanifest från CDN, som kan innehålla annonsradbrytningsinformation.
1. Manifestservern dirigerar om klienten till det överordnad/variantmanifest som den genererade för klienten.

   >[!NOTE]
   >
   >Om Bootstrap URL-frågeparametrarna innehåller inställningen `pttrackingmode=simple` eller `ptplayer=ios-mobileweb`, returnerar manifestservern den överordnad URL:en för variantmanifestet i ett JSON-objekt och klienten skickar en GET-begäran till variantmanifest-URL:en.

1. Klienten väljer en ström i det genererade variantmanifestet som ska spelas upp och skickar annonsinformation till manifestservern.
1. Manifestservern skickar informationen som klienten skickar till annonsservern och tar emot annonser och URL:er för annonsspårning från annonsservern. Om en angiven annons inte är i HLS-format skickar manifestservern den till CRS för konvertering till HLS.
1. Manifestservern sammanfogar annonser i innehållsmanifestet och skickar det nya sammanfogade manifestet till klienten.
1. Klienten spelar upp innehållet med de insydda annonserna och gör förfrågningar vid angivna tidpunkter till de angivna spårnings-URL:erna.

Primetime-annonsinfogning har stöd för klienter på många videoleveransplattformar. Alla klienter är inte baserade på Primetimes TVSDK-paket, men alla klienter skickar GET-begäranden till samma grundläggande URL. Frågeparametrar särskiljer en klientbegäran från en annan genom att tala om manifestservern:

* vilken klient som begär detta,
* vad kunden vill ha,
* och vilken annonsspårningsinformation som ska tillhandahållas.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

Manifestservern använder CORS (Cross-Origin Resource Sharing Standard). Det söker efter ett `Origin`-huvud i de begäranden det tar emot. Om rubriken finns, svarar den med

* `Access-Control-Allow-Origin: *`sträng från rubriken Ursprung`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

Annars svarar den med

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`