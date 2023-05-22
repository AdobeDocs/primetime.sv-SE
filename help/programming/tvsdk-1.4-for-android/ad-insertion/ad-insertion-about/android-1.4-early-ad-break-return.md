---
description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
title: Implementera en tidig radbrytning
exl-id: 38386ab7-0e3b-4628-84eb-470d585eb929
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# Implementera en tidig radbrytning {#implement-an-early-ad-break-return}

För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.

Till exempel kanske inte längden på annonsbrytningen i vissa sportevenemang är känd innan brytningen börjar. TVSDK anger en standardlängd, men om spelet återupptas innan pausen är slut måste annonsbrytningen avbrytas. Ett annat exempel är en nödsignal under en annonsbrytning i en liveström.

1. Prenumerera på splice out/in och annonsmarkörer ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`och `#EXT-X-CUE`).

   Mer information om hur du delar ut/in annonsmarkörer finns i [Generatorer för affärsmöjligheter och lösningar för innehåll](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. Använd en anpassad `ContentFactory`.
1. I `retrieveGenerators()`, använder du `SpliceInPlacementOpportunityGenerator`.

   Till exempel:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Mer information om hur du använder en anpassad `ContentFactory`, se steg 1 i [Implementera en anpassad affärsmöjlighetsdetektor](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. På samma anpassade `ContentFactory`, implementera `retrieveResolvers` och inkludera `AuditudeResolver` och `SpliceInCustomResolver`.

   Till exempel:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
