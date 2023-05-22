---
description: Webbläsare-TVSDK buffrar ibland videoströmmen för att ge en smidigare visning. Du kan konfigurera hur spelaren buffrar.
title: Buffring
exl-id: 786379d1-0f2d-44a9-b580-1c8dcbd3fd17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Buffring{#buffering}

Webbläsare-TVSDK buffrar ibland videoströmmen för att ge en smidigare visning. Du kan konfigurera hur spelaren buffrar.

Browser TVSDK definierar en uppspelningsbuffertlängd på minst 30 sekunder och en inledande bufferttid inom den, innan mediet börjar spelas upp, på minst 2 sekunder. Efter programanrop `play` men innan uppspelningen börjar buffras mediet med Browser TVSDK upp till den inledande tiden för att ge en jämn start när uppspelningen faktiskt börjar.

## Ange buffringstider {#section_179DA7CA865D48EBA4B03D50B6B7BC50}

MediaPlayer innehåller metoder för att ställa in och hämta den inledande buffringstiden och uppspelningsbuffringstiden.

>[!TIP]
>
>Om du inte anger parametrar för buffertkontroll innan uppspelningen startar, blir mediaspelaren som standard 2 sekunder för den inledande bufferten och 30 sekunder för den pågående uppspelningsbufferttiden.

* Om du vill använda buffertparametrarna använder du MediaPlayers `bufferControlParameters` -attribut.

   Om du till exempel vill ställa in den inledande bufferten på 2 sekunder och uppspelningsbufferttiden på 30 sekunder:

   ```js
   var params = new AdobePSDK.BufferControlParameters(2000, 30000);
   ```

## Buffringstidsregler {#section_7EF2947931654CCC8DAB9172391FA4EB}

Beroende på din miljö (inklusive enheten, operativsystemet eller nätverksförhållandena) kan du ange olika buffringsprinciper för spelaren, till exempel ändra minimilängden för inledande buffring och för pågående uppspelningsbuffring.

Efter att du har ringt `play`, börjar mediespelaren buffra videon. När mediespelaren har buffrat den mängd video som anges av den inledande buffringstiden börjar uppspelningen. Den här processen förbättrar starttiden eftersom spelaren inte väntar på att hela uppspelningsbufferten ska fyllas innan uppspelningen startas. Efter att de få inledande sekunderna har buffrats börjar uppspelningen i stället.

När videon återges fortsätter Browser TVSDK att buffra nya fragment tills den har buffrat den mängd som anges av uppspelningsbufferttiden. Om den aktuella buffertlängden sjunker under uppspelningsbuffertens tid hämtar spelaren ytterligare fragment. När den aktuella buffertlängden är över uppspelningsbufferttiden med några sekunder kommer Browser TVSDK att sluta hämta fragment.

>[!TIP]
>
>Om det inledande buffertvärdet är högt kan det ge användaren en lång inledande buffringstid innan start. Detta kan ge en jämnare uppspelning under en längre tid. Men om nätverksförhållandena är dåliga kan den inledande uppspelningen fördröjas.
