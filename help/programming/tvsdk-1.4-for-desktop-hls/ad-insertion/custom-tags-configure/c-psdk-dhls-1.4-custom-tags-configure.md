---
description: Medieströmmar kan innehålla ytterligare metadata i form av taggar i spellistan/manifestfilen, och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.
title: Egna taggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Egna taggar{#custom-tags}

Medieströmmar kan innehålla ytterligare metadata i form av taggar i spellistan/manifestfilen, och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.

## HLS-innehållstaggar {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Den här funktionen är inte tillgänglig för Safari på Apple-datorer eftersom TVSDK använder videotaggen i stället för Flash eller MSE för att spela upp HLS-innehåll.

TVSDK har körklart stöd för specifika #EXT-annonstaggar. Ditt program kan använda anpassade taggar för att förbättra arbetsflödet för annonsering eller för att stödja svartoutscenarier. För att stödja avancerade arbetsflöden kan du med TVSDK ange och prenumerera på ytterligare taggar i manifestet. Du kan meddelas när dessa taggar visas i manifestfilen.

>[!TIP]
>
>Du kan prenumerera på anpassade taggar både för VOD och live/linear-strömmar.

>[!NOTE]
>
>När HLS spelas upp med videotaggen i Safari, och inte med Flash Fallback, är den här funktionen inte tillgänglig i Safari.

## Använda anpassade HLS-taggar {#section_AD032318AEF5418393D2B1DF36B0BABB}

Här är ett exempel på en anpassad VOD-resurs:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

Programmet kan konfigurera följande scenarier:

* Ett meddelande när `#EXT-X-ASSET` -taggar, eller andra uppsättningar egna taggnamn som du har prenumererat på, finns i filen.
* Infoga annonser när en `#EXT-X-AD` -taggen, eller något annat anpassat taggnamn, finns i strömmen.

Du kan prenumerera på följande taggar som anpassade taggar: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Du får ett meddelande med `TimedMetadata` -händelsen vid parsning av manifestfiler.

Det finns några reklamtaggar, till exempel `EXT-X-CUE`som du redan prenumererar på. Dessa annonstaggar används också av standardgeneratorn för affärstillfällen. Du kan ange vilka annonstaggar som ska användas av standardgeneratorn för affärsmöjlighet genom att ange `adTags` -egenskap.
