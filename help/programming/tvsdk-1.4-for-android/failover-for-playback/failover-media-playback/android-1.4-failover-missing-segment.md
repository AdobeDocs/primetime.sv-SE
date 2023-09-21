---
description: När ett segment saknas, till exempel om ett visst segment inte kan hämtas, försöker återskapa det med hjälp av en mängd olika redundansförsök. Om det inte går att återställa genereras ett fel.
title: Segmentredundans saknas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Segmentredundans saknas{#missing-segment-failover}

När ett segment saknas, till exempel om ett visst segment inte kan hämtas, försöker återskapa det med hjälp av en mängd olika redundansförsök. Om det inte går att återställa genereras ett fel.

Om ett segment saknas på servern, till exempel på grund av att manifestfilen inte finns, kan segmentet inte laddas ned och så vidare, försöker TVSDK att redundansväxla genom att försöka med följande alternativ:

1. Försök med en växling vid fel till samma segment, med samma bithastighet, i en variantfil.
1. Växla till en alternativ bithastighet (ABR-switch) i samma fil.
1. Bläddra igenom alla tillgängliga bithastigheter i alla tillgängliga varianter.
1. Hoppa över segmentet och skicka en varning.

När TVSDK inte kan hämta ett alternativt segment utlöses en `CONTENT_ERROR` felmeddelande. Det här meddelandet innehåller ett internt meddelande med koden `DOWNLOAD_ERROR` kod. Om direktuppspelningen med problemet är ett alternativt ljudspår genereras `AUDIO_TRACK_ERROR` felmeddelande.

Om videomotorn inte kontinuerligt kan hämta segment begränsas antalet kontinuerliga segmenthopp till 5, varefter uppspelningen stoppas och en `NATIVE_ERROR` med koden 5.

>[!NOTE]
>
>ABR-styrparametrarna (Adaptive bit rate) beaktas inte när en växling vid fel inträffar. Detta beror på att failover-mekanismen är utformad för att använda någon av de spelningslistor som är tillgängliga, oavsett deras bithastighetsprofil, som säkerhetskopieringsströmmar.
>
>Under en redundansåtgärd kan det finnas en profilväxling. Om ett fel inträffar under hämtningen av ett av spellistsegmenten ignoreras ABR-kontrollparametrar som min/max tillåtna bithastighet.
