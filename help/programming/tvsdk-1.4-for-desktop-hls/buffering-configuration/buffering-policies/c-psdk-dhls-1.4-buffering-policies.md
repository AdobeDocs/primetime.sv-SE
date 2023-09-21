---
description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
title: Buffringstidsregler
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Buffringstidsregler {#buffering-time-policies}

TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.

TVSDK definierar en uppspelningsbuffertlängd på minst 30 sekunder och en inledande bufferttid inom denna, innan mediet börjar spelas upp, på minst 5 sekunder. Efter programanrop `play` men innan uppspelningen börjar buffrar TVSDK mediet tills det börjar spelas upp, vilket ger en mjuk start när uppspelningen börjar.

Du kan ändra bufferttiderna genom att definiera nya buffertprinciper.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Beroende på din miljö (inklusive enheten, operativsystemet eller nätverksförhållandena) kan du ange olika buffringsprinciper för spelaren, till exempel ändra minimilängden för inledande buffring och för pågående uppspelningsbuffring.

Efter att du har ringt `play`, börjar mediespelaren buffra videon. När mediespelaren har buffrat den mängd video som anges av den inledande buffringstiden börjar uppspelningen. Den här processen förbättrar starttiden eftersom spelaren inte väntar på att hela uppspelningsbufferten ska fyllas innan uppspelningen startas. Efter att de få inledande sekunderna har buffrats börjar uppspelningen i stället.

När videon återges fortsätter TVSDK att buffra nya fragment tills det har buffrat den mängd som anges av uppspelningsbufferttiden. Om den aktuella buffertlängden sjunker under uppspelningsbuffertens tid hämtar spelaren ytterligare fragment. När den aktuella buffertlängden är över uppspelningsbufferttiden med några sekunder kommer TVSDK att sluta hämta fragment.

>[!TIP]
>
>Om det inledande buffertvärdet är högt kan det ge användaren en lång inledande buffringstid innan start. Detta kan ge en mjuk uppspelning under en längre tid, men om nätverksförhållandena är dåliga kan den inledande uppspelningen fördröjas.
