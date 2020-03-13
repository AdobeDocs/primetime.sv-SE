---
description: Medieströmmar kan innehålla ytterligare metadata i form av taggar i spellistan/manifestfilen, och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.
seo-description: Medieströmmar kan innehålla ytterligare metadata i form av taggar i spellistan/manifestfilen, och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.
seo-title: Egna taggar
title: Egna taggar
uuid: 103f4fff-2218-4d44-90bc-b80da467f282
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Översikt {#custom-tags-overview}

Medieströmmar kan innehålla ytterligare metadata i form av taggar i spellistan/manifestfilen, och den här filen anger var annonsen placeras. Du kan ange egna taggnamn och få meddelanden när vissa taggar visas i manifestfilen.

## HLS-innehållstaggar {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Den här funktionen är inte tillgänglig för Safari på Apple-datorer eftersom TVSDK använder videotaggen i stället för Flash eller MSE för att spela upp HLS-innehåll.

TVSDK har körklart stöd för specifika #EXT-annonstaggar. Ditt program kan använda anpassade taggar för att förbättra arbetsflödet för annonsering eller för att stödja svartoutscenarier. Om du vill ha stöd för avancerade arbetsflöden kan du med TVSDK ange och prenumerera på ytterligare taggar i manifestet. Du kan meddelas när dessa taggar visas i manifestfilen.

>[!TIP]
>
>Du kan prenumerera på anpassade taggar både för VOD och live/linear-strömmar.

>[!NOTE] {othertype=&quot;Limitation&quot;}
>
>När HLS spelas upp med videotaggen i Safari, och inte med Flash Fallback, är den här funktionen inte tillgänglig i Safari.

## Använd anpassade HLS-taggar {#section_AD032318AEF5418393D2B1DF36B0BABB}

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