---
description: Om ditt system har tillgång till maskinvarustödd avkodning kan du få ett jämnare trick än med den rena programimplementeringen av TVSDK genom att använda iFrame-formatet.
seo-description: Om ditt system har tillgång till maskinvarustödd avkodning kan du få ett jämnare trick än med den rena programimplementeringen av TVSDK genom att använda iFrame-formatet.
seo-title: Smidigare tricks-play-åtgärder
title: Smidigare tricks-play-åtgärder
uuid: 4749bfa0-17bf-4444-a167-987249945325
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Smidigare tricks-play-åtgärder {#smoother-trick-play-operations}

Om ditt system har tillgång till maskinvarustödd avkodning kan du få ett jämnare trick än med den rena programimplementeringen av TVSDK genom att använda iFrame-formatet.

<!--<a id="section_3DBFD7A3D1C7453096D3D3885E786263"></a>-->

Om du använder iFrame-formatet blir resultatet trippelåtgärder som inte är jämna. En mjukare trickåtgärd använder en normal (inte iFrame) profil, stöd för maskinvaruavkodning och en högre bildrutefrekvens. Olika maskinvarustödda avkodningsenheter har olika funktioner. Dubbelhastighet kräver 60 bildrutor per sekund (FPS) och fyrdubbel hastighet kräver 120 bildrutor/s.

>[!IMPORTANT]
>
>Adobe rekommenderar att du begränsar uppspelningen till dubbel hastighet för nyare Android-enheter och inte använder funktionen för äldre Android-enheter.

För att få jämnare tricks-uppspelning ställer du in `ABRControlParameters.maxPlayoutRate` till önskad multipel av normal hastighet (till exempel 2.0 för dubbel hastighet). Om ett efterföljande anrop till `MediaPlayer.setRate()` har ett argument som är mindre än eller lika med det värde du anger för `maxPlayoutRate`, använder TVSDK en normal profil för att få en jämnare trickfunktion. I annat fall används en iFrame-profil för trickåtgärden.
