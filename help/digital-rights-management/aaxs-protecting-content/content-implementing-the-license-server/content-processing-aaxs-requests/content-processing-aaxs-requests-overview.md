---
seo-title: Översikt
title: Översikt
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Översikt{#overview}

Det allmänna sättet att hantera begäranden är att skapa en hanterare, analysera begäran, ange svarsdata eller felkod och stänga hanteraren.

Basklassen som används för att hantera en begäran/svar-interaktion är `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. En instans av `HandlerConfiguration` klassen används för att initiera hanteraren. `HandlerConfiguration` lagrar information om serverkonfiguration, inklusive transportreferenser, tolerans för tidsstämpling, listor för principuppdatering och återkallningslistor. Hanteraren läser informationen i begäran och tolkar begäran till en instans av `RequestMessageBase`. Anroparen kan granska informationen i begäran och avgöra om ett fel eller ett svar ska returneras (underklasser till att `RequestMessageBase` tillhandahålla en metod för att ange svarsdata).

Om begäran lyckas, ange svarsdata. Anropar annars `RequestMessageBase.setErrorData()` vid fel. Avsluta alltid implementeringen genom att anropa `close()` metoden (det rekommenderas att `close()` anropas i `finally` blocket för en `try` programsats). I API-referensdokumentationen finns ett exempel `MessageHandlerBase` på hur du anropar hanteraren.

>[!NOTE]
>
>HTTP-statuskod 200 (OK) ska skickas som svar på alla begäranden som behandlas av hanteraren. Om hanteraren inte kunde skapas på grund av ett serverfel kan servern svara med en annan statuskod, till exempel 500 (Internt serverfel).

Klienten använder den licensserveradress som angavs vid paketeringen som bas-URL för alla begäranden som skickas till licensservern. Om server-URL:en till exempel anges som &quot;<span></span>https://licenseserver.com/path&quot; skickar klienten begäranden till &quot;<span></span>https://licenseserver.com/path/flashaccess/...&quot;. I följande avsnitt finns mer information om den specifika sökvägen som används för varje typ av begäran. När du implementerar din licensserver måste servern svara på de sökvägar som krävs för varje typ av begäran.

En licensbegäran kan innehålla en autentiseringstoken. Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genererad av `AuthenticationHandler`och SDK:n ser till att token är giltig innan en licens utfärdas.
