---
description: Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.
title: Skapa ett kontrollfält förbättrat för DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Skapa ett kontrollfält förbättrat för DVR{#construct-a-control-bar-enhanced-for-dvr}

Du kan implementera ett kontrollfält med DVR-stöd för VOD och direktuppspelning. DVR-stödet innefattar begreppet sökbart fönster och klientens direktpunkt.

* För VOD är längden på det sökbara fönstret längden på hela resursen.
* För direktuppspelning definieras längden på DVR-fönstret (sökbart) som det tidsintervall som börjar vid direktuppspelningsfönstret och slutar vid klientens direktpunkt.

   Klientens direktpunkt beräknas genom att den buffrade längden subtraheras från livefönstrets slut. Målets varaktighet är ett värde som är större än eller lika med den maximala längden för ett fragment i manifestet.

   Kontrollfältet för direktuppspelning stöder DVR genom att först placera tummen vid klientens direktpunkt när uppspelningen startar och genom att visa ett område som markerar det område där sökning inte är tillåten.

För ett kontrollfält:

1. Lägg till en övertäckning i kontrollfältet som representerar uppspelningsintervallet.

1. När användaren börjar söka kontrollerar du om den önskade sökpositionen ligger inom det sökbara intervallet.
