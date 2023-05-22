---
title: Just-in-Time Transcoding
description: Just-in-Time Transcoding
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Just-in-Time Transcoding {#just-in-time-transcoding}

Primetime Ad Insertion har just-in-time-transkodning och paketering för att säkerställa att inkompatibla annonskreatörer kan spelas upp korrekt i innehållsströmmar. Det kan även injicera ID3-paket i annonsfragment som kan användas i annonsspårning på klientsidan.
Ett typiskt arbetsflöde är följande:

1. Adobe Primetime Ad Insertion hämtar annonser/kreatörer från kundens annonsserver.

1. Om annonsens kreativa format är direkt kompatibelt med innehållsströmmen infogas den kreativa delen i manifestet.

1. Om annonsens kreativa format inte är direkt kompatibelt (t.ex. .mp4, .mov, .webm) söker Primetime Ad Insertion efter en förkodad version av annonsen från ett angivet CDN. Om en annons hittas ska den läggas in. I annat fall står annonsen i kö för transkodning.

1. När annonsen har omkodats kommer Primetime Ad Insertion att knyta alla efterföljande förfrågningar om annonsen till manifesten.

Primetime Ad Insertion stöder omkodning för de flesta video- och linjära format. Annonstranschering sker vanligtvis på mindre än tre minuter. Kontakta din supportrepresentant på Primetime om du vill ha mer information.
