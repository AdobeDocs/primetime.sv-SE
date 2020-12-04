---
description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
seo-description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
seo-title: Implementera en tidig radbrytning
title: Implementera en tidig radbrytning
uuid: 41b70ee1-290b-4732-899e-32b234ec1d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---


# Implementera en tidig annonsradbrytning {#implement-an-early-ad-break-return}

För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.

Till exempel kanske inte längden på annonsbrytningen i vissa sportevenemang är känd innan brytningen börjar. TVSDK anger en standardlängd, men om spelet återupptas innan pausen är slut måste annonsbrytningen avbrytas. Ett annat exempel är en nödsignal under en annonsbrytning i en liveström.

1. Prenumerera på splice out/in-annonsmarkörerna ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` och `#EXT-X-CUE`).

   Mer information om hur du delar ut/in annonsmarkörer finns i [Affärsgeneratorer och innehållslösare](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. Använd en anpassad `ContentFactory`.
1. I `retrieveGenerators()` använder du `SpliceInPlacementOpportunityGenerator`.

   Exempel:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Mer information om hur du använder en anpassad `ContentFactory` finns i steg 1 i [Implementera en anpassad affärsmöjlighetsdetektor](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md).

1. Implementera `retrieveResolvers` och inkludera `AuditudeResolver` och `SpliceInCustomResolver` på samma anpassade `ContentFactory`.

   Exempel:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

