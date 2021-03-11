---
description: För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.
title: Implementera en tidig radbrytning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

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

