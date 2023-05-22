---
description: Om ditt system har tillgång till maskinvarustödd avkodning kan du få ett jämnare trick än med den rena programimplementeringen av TVSDK genom att använda iFrame-formatet.
title: Smidigare tricks-play-åtgärder
exl-id: f69bf480-122b-474d-8f35-31655ea87c70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Smidigare tricks-play-åtgärder {#smoother-trick-play-operations}

Om ditt system har tillgång till maskinvarustödd avkodning kan du få ett jämnare trick än med den rena programimplementeringen av TVSDK genom att använda iFrame-formatet.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

Om du använder iFrame-formatet blir resultatet trippelåtgärder som inte är jämna. En mjukare trickåtgärd använder en normal (inte iFrame) profil, stöd för maskinvaruavkodning och en högre bildrutefrekvens. Olika maskinvarustödda avkodningsenheter har olika funktioner. Dubbelhastighet kräver 60 bildrutor per sekund (FPS) och fyrdubbel hastighet kräver 120 bildrutor/s.

>[!IMPORTANT]
>
>Adobe rekommenderar att du begränsar uppspelningen till dubbel hastighet för nyare Android-enheter och inte använder funktionen för äldre Android-enheter.

För att få ett jämnare tricks ska du ställa in `ABRControlParameters.maxPlayoutRate` till önskad multipel av normal hastighet (till exempel 2.0 för dubbel hastighet). Om ett efterföljande anrop till `MediaPlayer.setRate()` har ett argument som är mindre än eller lika med det värde du anger för `maxPlayoutRate`, använder TVSDK en normal profil för att få ett jämnare trickspel. I annat fall används en iFrame-profil för trickåtgärden.
