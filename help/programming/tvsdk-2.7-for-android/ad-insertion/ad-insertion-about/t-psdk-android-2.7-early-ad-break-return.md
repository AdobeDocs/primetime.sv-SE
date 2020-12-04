---
description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
seo-description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
seo-title: Implementera en tidig radbrytning
title: Implementera en tidig radbrytning
uuid: c67f2158-5df4-458c-a27a-6329c5d26638
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# Implementera en tidig annonsradbrytning {#implement-an-early-ad-break-return}

För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.

Till exempel kanske inte längden på annonsbrytningen i vissa sportevenemang är känd innan brytningen börjar. TVSDK anger en standardlängd, men om spelet återupptas innan pausen är slut måste annonsbrytningen avbrytas. Ett annat exempel är en nödsignal under en annonsbrytning i en liveström.

1. Prenumerera på `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` och `#EXT-X-CUE`, som är delningstiden i markörer.

   Mer information om hur du delar ut/in annonsmarkörer finns i [Affärsgeneratorer och innehållslösare](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

1. Använd en anpassad `ContentFactory`.
1. I `retrieveGenerators` använder du `SpliceInPlacementOpportunityGenerator`.

   Exempel:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Mer information om hur du använder en anpassad `ContentFactory` finns i steg 1 i [Implementera en anpassad affärsmöjlighetsgenerator](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. Implementera `retrieveResolvers` och inkludera `AuditudeResolver` och `SpliceInCustomResolver` på samma anpassade `ContentFactory`.

   Exempel:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

