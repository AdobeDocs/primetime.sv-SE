---
title: Bootstrap API
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Bootstrap API {#bootstrap-api}

Obligatoriska parametrarGenerera en bootstrap

## Parameterbeskrivning {#parameter-description}

| parameter | description | format |
|---|---|---|
| pabimode | Aktiverar [delvis infogning](ad-insertion-live-linear-stream.md#partial-ad-break-support) av annonsradbrytningar för liveströmmar. Möjliga värden: true för att aktivera inaktivering (standard inaktiverat) | HLS/DASH |
| ptadwindow | Varaktighet (i sekunder) för fönstret för uppslag och beslut - hur långt tillbaka Primetime Ad Insertion kommer att leta efter reklamtips när en DVR-användare ansluter till strömmen. Värdet noll inaktiverar annonsbeslut i mellanrullen i det inledande manifestet, och beslut återupptas först efter den första uppdateringen. Den här parametern är användbar för att inaktivera annonsinfogning i sessioner som bara kan vara i några sekunder (även kanalvänd). Möjliga värden: numerisk sträng 0-1800 (standard 1800) | Endast HLS |
| ptassetid | Unikt ID för innehållet som tilldelas och underhålls av utgivaren.  Krävs när det används tillsammans med Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Lista över ett eller flera CDN:er som ska vara värd för omkodade resurser. Mer information finns i [Multi CDN-stöd](multi-cdn-support.md). Möjliga värden: akamai, level3, llnw (limelight network), comcastSom standard används Primetime Ad Insertion CDN:er | HLS/DASH |
| ptcueformat | Det angivna formatet för taggar som ska utföra annonsbeslut (till exempel scte35). Möjliga värden: dpisimple, dpiscte35, elemental For custom cue formats formats, please contact your technical account manager for the value to use for your use case | HLS/DASH |
| ptfailover | Signalerar manifestservern för att identifiera primära strömmar och failover-strömmar som anges i den överordnad spellistan och för att behandla dem som osammanhängande uppsättningar. Detta underlättar redundans och förhindrar timingfel. (Endast för Apple HLS-enheter.) Mer information finns i [Underlätta växling av HLS-spelare](hls-switching-to-failover.md) | Endast HLS |
| ptmulticall | Om det här alternativet är aktiverat görs en separat annonsbegäran för varje tillgång som hittas i en VOD-resurs.  Som standard försöker Primetime Ad Insertion samla in all tillgänglig information och skicka den till annonsservern i en begäran. Möjliga värden: true för att aktivera inaktivering (standard inaktiverat) | HLS/DASH |
| ptagds | Aktiverar inmatning av EXT-X-DISCONTINUITY-SEQUENCE-taggar i HLS-rubriker.Möjliga värden:true för att inaktivera (standard inaktiverat) | Endast HLS |
| pttimeline | En sträng som innehåller den önskade tidslinjen för annonsplacering och innehåll, som åsidosätter och bryter i innehållsströmmen. [ Se VOD-tidslinjeformat ] | HLS/DASH |
| pttoken | Aktiverar tokenskyddsscheman för innehållsfragment-/segmentauktoriseringstoken för CDN:er Möjliga värden: akamai, llnw (limelight), ctl (centurylink) (standardtokenisering är inaktiverat) | HLS/DASH |
| pttrackingmode | Aktivera annonsspårningsscheman:Möjliga värden:enkla för klient- och spårningsprogram för serversidesbaserade och enkla spårningsmetoder för hybridklient-/serverannonser (som standard utförs ingen annonsspårning) | HLS/DASH |
| pttrackingversion |  |  |
| ptadtimeout (som i 20.9.2) |  |  |
| ptparallelstream (som i 20.9.3) |  |  |
