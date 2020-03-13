---
description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
seo-description: TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.
seo-title: Buffringstidsregler
title: Buffringstidsregler
uuid: 8d3ce9be-cca4-485e-ba66-d2f2aa6822dd
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Buffringstidsregler {#buffering-time-policies}

TVSDK buffrar ibland videoströmmen för att ge en jämnare tittarupplevelse. Du kan konfigurera hur spelaren buffrar.

TVSDK definierar en uppspelningsbuffertlängd på minst 30 sekunder och en inledande bufferttid inom denna, innan mediet börjar spelas upp, på minst 5 sekunder. När programmet har anropat `play` men innan uppspelningen börjar buffrar TVSDK mediet till den inledande tiden för att ge en jämn start när uppspelningen faktiskt börjar.

Du kan ändra bufferttiderna genom att definiera nya buffertprinciper.

<!--<a id="section_F6EEE15600814A70A57CCBACE20D68BD"></a>-->

Beroende på din miljö (inklusive enheten, operativsystemet eller nätverksförhållandena) kan du ange olika buffringsprinciper för spelaren, till exempel ändra minimilängden för inledande buffring och för pågående uppspelningsbuffring.

När du har anropat `play`börjar mediespelaren buffra videon. När mediespelaren har buffrat den mängd video som anges av den inledande buffringstiden börjar uppspelningen. Den här processen förbättrar starttiden eftersom spelaren inte väntar på att hela uppspelningsbufferten ska fyllas innan uppspelningen startas. Efter att de få inledande sekunderna har buffrats börjar uppspelningen i stället.

När videon återges fortsätter TVSDK att buffra nya fragment tills det har buffrat den mängd som anges av uppspelningsbufferttiden. Om den aktuella buffertlängden sjunker under uppspelningsbuffertens tid hämtar spelaren ytterligare fragment. När den aktuella buffertlängden är över uppspelningsbufferttiden med några sekunder kommer TVSDK att sluta hämta fragment.

>[!TIP]
>
>Om det inledande buffertvärdet är högt kan det ge användaren en lång inledande buffringstid innan start. Detta kan ge en jämnare uppspelning under en längre tid. Men om nätverksförhållandena är dåliga kan den inledande uppspelningen fördröjas.

