---
description: När ett segment saknas, till exempel om ett visst segment inte kan hämtas, försöker återskapa det med hjälp av en mängd olika redundansförsök. Om det inte går att återställa genereras ett fel.
seo-description: När ett segment saknas, till exempel om ett visst segment inte kan hämtas, försöker återskapa det med hjälp av en mängd olika redundansförsök. Om det inte går att återställa genereras ett fel.
seo-title: segmentredundans saknas
title: segmentredundans saknas
uuid: 17ee1221-e1eb-4f64-a406-4d7eff1d7555
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# segmentredundans saknas{#missing-segment-failover}

När ett segment saknas, till exempel om ett visst segment inte kan hämtas, försöker återskapa det med hjälp av en mängd olika redundansförsök. Om det inte går att återställa genereras ett fel.

Om ett segment saknas på servern, till exempel på grund av att manifestfilen inte finns, kan segmentet inte laddas ned och så vidare, försöker TVSDK att redundansväxla genom att försöka med följande alternativ:

1. Försök med en växling vid fel till samma segment, med samma bithastighet, i en variantfil.
1. Växla till en alternativ bithastighet (ABR-switch) i samma fil.
1. Bläddra igenom alla tillgängliga bithastigheter i alla tillgängliga varianter.
1. Hoppa över segmentet och skicka en varning.

När TVSDK inte kan hämta ett alternativt segment utlöses ett `CONTENT_ERROR` felmeddelande. Det här meddelandet innehåller ett internt meddelande med `DOWNLOAD_ERROR` koden. Om strömmen med problemet är ett alternativt ljudspår genereras felmeddelandet `AUDIO_TRACK_ERROR` .

Om videomotorn inte kontinuerligt kan hämta segment begränsas antalet kontinuerliga segmenthopp till 5, varefter uppspelningen stoppas och en `NATIVE_ERROR` åtgärd med koden 5 utfärdas.

>[!NOTE]
>
>ABR-styrparametrarna (Adaptive bit rate) beaktas inte när en växling vid fel inträffar. Detta beror på att failover-mekanismen är utformad för att använda någon av de spelningslistor som är tillgängliga, oavsett deras bithastighetsprofil, som säkerhetskopieringsströmmar.
>
>Under en redundansåtgärd kan det finnas en profilväxling. Om ett fel inträffar under hämtningen av ett av spellistsegmenten ignoreras ABR-kontrollparametrar som min/max tillåtna bithastighet.

