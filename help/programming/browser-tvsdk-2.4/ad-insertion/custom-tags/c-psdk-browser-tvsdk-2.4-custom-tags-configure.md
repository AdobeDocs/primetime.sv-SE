---
description: Medieströmmar kan innehålla ytterligare metadata i form av taggar i MPD-filen (Media Presentation Description), och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.
seo-description: Medieströmmar kan innehålla ytterligare metadata i form av taggar i MPD-filen (Media Presentation Description), och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.
seo-title: Egna taggar
title: Egna taggar
uuid: d1e34288-545b-440f-a262-2fb853f0e3c4
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Översikt {#custom-tags-overview}

Medieströmmar kan innehålla ytterligare metadata i form av taggar i MPD-filen (Media Presentation Description), och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.

## HLS-innehållstaggar {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Den här funktionen är inte tillgänglig för Safari på Apple-datorer, eftersom Browser TVSDK använder videotaggen i stället för Flash eller MSE för att spela upp HLS-innehåll.

Browser TVSDK har körklart stöd för specifika #EXT-annonstaggar. Ditt program kan använda anpassade taggar för att förbättra arbetsflödet för annonsering eller för att stödja svartoutscenarier. Om du vill ha stöd för avancerade arbetsflöden kan du med Browser TVSDK ange och prenumerera på ytterligare taggar i manifestet. Du kan meddelas när dessa taggar visas i manifestfilen.

>[!TIP]
>
>Du kan prenumerera på anpassade taggar både för VOD och live/linear-strömmar.

>[!NOTE] {othertype=&quot;Limitation&quot;}
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

* Ett meddelande när det finns `#EXT-X-ASSET` taggar, eller andra uppsättningar anpassade taggnamn som du prenumererar på, i filen.
* Infoga annonser när en `#EXT-X-AD` tagg eller något annat anpassat taggnamn hittas i strömmen.

Du kan prenumerera på följande taggar som anpassade taggar: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`.. Du meddelas om en `TimedMetadata` händelse under parsning av manifestfiler.

Det finns några reklamtaggar, till exempel `EXT-X-CUE`, som du redan prenumererar på. Dessa annonstaggar används också av standardgeneratorn för affärstillfällen. Du kan ange vilka annonstaggar som ska användas av standardgeneratorn för affärsmöjlighet genom att ange `adTags` egenskapen.

## DASH-innehållstaggar {#section_967A952319BE4048B4C6612FFF7ADA6E}

DASH har två sätt att signalera händelser:

* I MPD-filen.

   Den här filen liknar M3U8-filen i HLS-innehåll och MPD-händelser finns i .mpd-filen.
* Inband i representationen

   Inband-händelser multiplexas med representationer genom att händelsemeddelandena läggs till som en del av segmenten. En representation är en lista över video- och ljudsegment som spelas upp i sekvens. Inband-händelsedata är inbäddade i dessa segment.

Dessa händelser meddelas som händelser till programmet så snart de tolkas av Browser TVSDK. `TimedMetadata` När en händelse har meddelats kommer den inte att meddelas igen.
