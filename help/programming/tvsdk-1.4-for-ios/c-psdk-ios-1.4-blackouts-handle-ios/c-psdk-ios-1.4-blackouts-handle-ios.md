---
description: TVSDK hanterar strömavbrott i livevideoströmmar och tillhandahåller alternativt innehåll under ett strömavbrott.
title: Hantera strömavbrott
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Hantera strömavbrott{#handle-blackouts-in-live-streams}

TVSDK hanterar strömavbrott i livevideoströmmar och tillhandahåller alternativt innehåll under ett strömavbrott.

Det vanligaste användningsexemplet som är kopplat till en programmeringsläcka är när din spelarapp tillhandahåller alternativt innehåll till användare som inte är berättigade att titta på huvudströmmen. Den här appen kan använda TVSDK för att fastställa början och slutet av den svarta out-perioden. På så sätt kan uppspelningen, i början av den svarta punkten, växla från huvudströmmen till en alternativ ström och sedan växla tillbaka till huvudströmmen när den svarta perioden är slut.

Så här implementerar du lösningen för detta användningsfall:

1. Konfigurera din app för att prenumerera på taggar för strömavbrott i ett liveströmmanifest.

   TVSDK känner inte direkt till svarta out-taggar, men det gör att din app kan prenumerera på meddelanden när specifika taggar påträffas under parsning av manifestfiler.
1. Lägg till en meddelandeavlyssnare för `PTTimedMetadataChangedNotification`.

   Det här meddelandet skickas varje gång en prenumerationstagg tolkas i manifestet och en ny `PTTimedMetadata` är förberedd från den.

1. Implementera en avlyssnarmetod, som `onMediaPlayerSubscribedTagIdentified`, för `PTTimedMetadata` objekt i förgrunden.

1. Varje gång det finns en uppdatering under uppspelningen använder du `PTMediaPlayerTimeChangeNotification` avlyssnare som ska hantera `PTTimedMetadata` objekt.

1. Lägg till `PTTimedMetadata` hanterare.

   Med den här hanteraren kan du växla till alternativt innehåll och gå tillbaka till huvudinnehållet som anges av `PTTimedMetadata` objekt och dess uppspelningstid.

1. Använd `onSubscribedTagInBackground` för att implementera avlyssnarmetoden för `PTTimedMetadata` objekt i bakgrunden.

   Den här metoden övervakar timingen i bakgrundsströmmen, vilket hjälper dig att avgöra när du kan växla från alternativt innehåll tillbaka till huvudinnehållet.

1. Implementera en avlyssnarmetod för bakgrundsfel.
1. Om det svarta området finns i DVR-spelaren i uppspelningsströmmen uppdaterar du de intervall som inte kan sökas.

   Programmet måste ange det icke sökbara intervallet i DVR:n i följande fall:

   * När du ansluter till huvudströmmen när en strömavtryckning finns i DVR:n.
   * När du växlar tillbaka till huvudinnehållet från det alternativa innehållet.
