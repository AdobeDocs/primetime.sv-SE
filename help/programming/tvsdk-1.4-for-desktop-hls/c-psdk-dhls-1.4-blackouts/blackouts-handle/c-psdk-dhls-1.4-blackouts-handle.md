---
description: Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.
seo-description: Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.
seo-title: Hantera strömavbrott i liveströmmar
title: Hantera strömavbrott i liveströmmar
uuid: df933087-c8a8-49eb-a016-6dfd971c219c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Hantera strömavbrott i liveströmmar{#handle-blackouts-in-live-streams}

Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.

När en strömbrytning inträffar i en liveström använder spelaren händelsehanterare för att upptäcka strömmen och ge alternativt innehåll till de användare som inte är berättigade att titta på huvudströmmen. Spelaren känner av start- och slutpunkten för den utblinda perioden, växlar uppspelningen från huvudströmmen till en alternativ ström och växlar tillbaka till huvudströmmen när den utsläckta perioden är slut.

I din klientapp prenumererar du på taggar för utsvärtning i TVSDK. När du får ett meddelande om nya *tidsbestämda metadataobjekt* , tolkar du tidsbestämda metadata-objektets data för att identifiera om objektet indikerar en tidsbegränsad inmatning eller en avslutning. För identifierade strömavbrott anropar du de relevanta TVSDK-elementen för att växla till alternativt innehåll i början av strömavbrottet och återigen för att återgå till huvudinnehållet när strömavbrottet är över.

>[!TIP]
>
>Nycklarna hämtas fortfarande från manifestet innan innehållet spelas upp.

När en användare ansluter till en liveström efter att utströmningsperioden är slut, och rullar tillbaka i tiden till den utblåsta perioden, spelas innehållet upp.

>[!IMPORTANT]
>
>Om alla nyckelbegäranden misslyckas genereras ett fel när manifestet analyseras. Om vissa förfrågningar misslyckas och vissa lyckas, försöker TVSDK att spela upp innehållet. Om TVSDK försöker spela upp en del av innehållet, men det inte finns någon giltig nyckel för att dekryptera innehållet, returneras ett fel.

För att hantera strömavbrott i liveströmmar:

1. Konfigurera appen för att identifiera svarta out-taggar genom att prenumerera på svarta out-taggar i ett live-stream-manifest.

   TVSDK upptäcker inte ensam strömslutningstaggar. du måste prenumerera på utmattningstaggar för att få ett meddelande när taggarna påträffas under tolkningen av manifestfilen.
1. Skapa händelseavlyssnare för taggar som spelaren prenumererar på.

   När en tagg inträffar som spelaren har prenumererat på (till exempel en out-tagg) i antingen förgrunden (huvudinnehåll) eller bakgrundsströmmanifest (alternativt innehåll), skickar TVSDK en `TimedMetadataEvent` tagg och skapar en `TimedMetadataObject` för `TimedMetadataEvent`.
1. Implementera hanterare för tidsbestämda metadatahändelser för både förgrunds- och bakgrundsströmmarna.

   I de här hanterarna hämtar du start- och sluttider för utmörningsperioden från tidsbestämda metadatahändelseobjekt.
1. Förbered `MediaPlayer` för strömavbrott.

   När `MediaPlayer` objektet försätts i läget FÖRBEREDD beräknar du och förbereder de svarta områdena och ställer in dem på `MediaPlayer` objektet.

1. För varje uppdatering av spelhuvudets position ska du kontrollera listan med `TimedMetadataObjects`.

   Det är här spelaren upptäcker den svarta start och slut och spårar tidpunkten för den svarta punkten när den inträffar.

1. Skapa metoder för att växla innehåll i början och slutet av den svarta punkten.

   När utströmningsperioden börjar växlar du huvudinnehållet till bakgrunden och växlar det alternativa innehållet till huvudströmmen. Fortsätt att hämta och tolka det ursprungliga manifestet i bakgrunden och fortsätt att söka efter sluttaggen för utmörkning, så att spelaren kan återansluta till den ursprungliga strömmen när utsläckningen är slut.

