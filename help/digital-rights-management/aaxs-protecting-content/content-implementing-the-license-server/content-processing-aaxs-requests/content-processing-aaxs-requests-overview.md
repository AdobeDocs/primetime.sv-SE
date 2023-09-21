---
title: Ökning
description: Ökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Ökning{#overview}

Det allmänna sättet att hantera begäranden är att skapa en hanterare, analysera begäran, ange svarsdata eller felkod och stänga hanteraren.

Den basklass som används för att hantera en begäran/svar-interaktion är `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. En instans av `HandlerConfiguration` -klassen används för att initiera hanteraren. `HandlerConfiguration` lagrar information om serverkonfiguration, inklusive transportreferenser, tolerans för tidsstämpling, listor för principuppdatering och återkallningslistor. Hanteraren läser informationen i begäran och tolkar begäran till en instans av `RequestMessageBase`. Anroparen kan granska informationen i begäran och avgöra om ett fel eller ett svar ska returneras (underklasser till `RequestMessageBase` tillhandahåller en metod för att ställa in svarsdata).

Om begäran lyckas anger du svarsdata. Anropa annars `RequestMessageBase.setErrorData()` vid fel. Avsluta alltid implementeringen genom att anropa `close()` metod (vi rekommenderar att `close()` anropas i `finally` block av `try` -programsats). Se `MessageHandlerBase` API-referensdokumentation som innehåller ett exempel på hur hanteraren anropas.

>[!NOTE]
>
>HTTP-statuskod 200 (OK) ska skickas som svar på alla begäranden som behandlas av hanteraren. Om hanteraren inte kunde skapas på grund av ett serverfel kan servern svara med en annan statuskod, till exempel 500 (Internt serverfel).

Klienten använder den licensserveradress som angavs vid paketeringen som bas-URL för alla begäranden som skickas till licensservern. Om server-URL:en anges som &quot;ht<span></span>tps://licenseserver.com/path&quot; skickar klienten begäranden till &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/..&quot;. I följande avsnitt finns mer information om den specifika sökvägen som används för varje typ av begäran. När du implementerar din licensserver måste servern svara på de sökvägar som krävs för varje typ av begäran.

En licensbegäran kan innehålla en autentiseringstoken. Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genereras av `AuthenticationHandler`och SDK:n ser till att token är giltig innan en licens utfärdas.
