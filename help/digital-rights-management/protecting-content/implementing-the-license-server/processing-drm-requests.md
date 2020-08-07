---
seo-title: Bearbeta Adobe Primetime DRM-begäranden
title: Bearbeta Adobe Primetime DRM-begäranden
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# Bearbeta Adobe Primetime DRM-begäranden {#process-adobe-primetime-drm-requests}

Det allmänna sättet att hantera begäranden är att skapa en hanterare, tolka begäran, ange svarsdata eller felkod och stänga hanteraren.

Basklassen som används för att hantera en begäran/svar-interaktion är `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. En instans av `HandlerConfiguration` klassen används för att initiera hanteraren. `HandlerConfiguration` lagrar information om serverkonfiguration, inklusive transportreferenser, tolerans för tidsstämpling, listor för principuppdatering och återkallningslistor. Hanteraren läser informationen i begäran och tolkar begäran till en instans av `RequestMessageBase`. Anroparen kan granska informationen i begäran och avgöra om ett fel eller ett svar ska returneras (underklasser till att `RequestMessageBase` tillhandahålla en metod för att ange svarsdata).

Om begäran lyckas, ange svarsdata. Anropar annars `RequestMessageBase.setErrorData()` vid fel. Avsluta alltid implementeringen genom att anropa `close()` metoden (det rekommenderas att `close()` anropas i `finally` blocket för en `try` programsats). I API-referensdokumentationen finns ett exempel `MessageHandlerBase` på hur du anropar hanteraren.

>[!NOTE]
>
>HTTP-statuskod 200 (OK) ska skickas som svar på alla begäranden som behandlas av hanteraren. Om hanteraren inte kunde skapas på grund av ett serverfel kan servern svara med en annan statuskod, till exempel 500 (Internt serverfel).

Klienten använder den licensserveradress som angavs vid paketeringen som bas-URL för alla begäranden som skickas till licensservern. Om server-URL:en till exempel anges som &lt;[!DNL ht<span></span>tps://licenseserver.com/path]> skickar klienten begäranden till &lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]> Se följande avsnitt för information om den specifika sökvägen som används för varje typ av begäran. När du implementerar din licensserver måste servern svara på de sökvägar som krävs för varje typ av begäran.

En licensbegäran kan innehålla en autentiseringstoken. Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genererad av `AuthenticationHandler`och SDK:n ser till att token är giltig innan en licens utfärdas.

## Använd datoridentifierare {#use-machine-identifiers}

Alla Adobe Primetime DRM-begäranden (med undantag för begäranden som stöder FMRMS-kompatibilitet) innehåller information om den maskintoken som har utfärdats till klienten under personaliseringen. Datortoken innehåller ett dator-ID, som är en identifierare som har tilldelats under personaliseringen. Du kan använda den här identifieraren för att räkna antalet datorer från vilka en användare har begärt en licens eller anslutit till en domän.

Du kan använda en identifierare på följande sätt:

* Metoden returnerar `getUniqueId()` en sträng som har tilldelats en enhet under personaliseringen. Du kan lagra strängarna i en databas och söka efter identifierare. Den här identifieraren ändras emellertid om användaren formaterar om hårddisken och anpassar den igen. Den här identifieraren har också ett annat värde mellan Adobe AIR och Adobe Flash Player i olika webbläsare på samma dator.
* Om du vill räkna datorer mer korrekt kan du använda `getBytes()` för att lagra hela identifieraren. Om du vill avgöra om datorn har setts tidigare hämtar du alla identifierare för ett användarnamn och anropar `matches()` för att kontrollera om det finns några matchningar. Eftersom metoden måste användas för att jämföra de värden som returneras av `matches()` `MachineId.getBytes`är detta alternativ endast praktiskt när det finns ett litet antal värden att jämföra. till exempel de datorer som är kopplade till en viss användare.

## Användarautentisering {#user-authentication}

En Adobe Primetime DRM-begäran kan innehålla en autentiseringstoken.

Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genererad av `AuthenticationHandler`. Om du vill komma åt och verifiera token måste du använda `RequestMessageBase.getAuthenticationToken()`. Om du vill initiera en begäran om användarnamn/lösenord på klienten använder du API:t för `DRMManager.authenticate()` ActionScript eller iOS.

Om klienten och servern använder en anpassad autentiseringsmekanism hämtar klienten en autentiseringstoken via någon annan kanal och ställer in en anpassad autentiseringstoken med API:t `DRMManager.setAuthenticationToken` ActionScript 3.0. Använd `RequestMessageBase.getRawAuthenticationToken()` för att hämta den anpassade autentiseringstoken. Serverimplementeringen avgör om den anpassade autentiseringstoken är giltig.

## Uppspelningsskydd {#replay-protection}

Om du vill återuppspela skydd kanske du vill kontrollera om meddelandeidentifieraren har setts nyligen genom att ringa `RequestMessageBase.getMessageId()`. I så fall kan en angripare försöka att upprepa begäran, vilket bör nekas. Servern kan identifiera uppspelningsförsök genom att lagra en lista över nyligen visade meddelande-ID:n och kontrollera varje inkommande begäran mot den cachelagrade listan. Om du vill begränsa hur lång tid som meddelandeidentifierarna måste lagras, anropar du `HandlerConfiguration.setTimestampTolerance()`. Om den här egenskapen är inställd nekas SDK sedan en begäran som har en tidsstämpel i mer än det angivna antalet sekunder av servertiden.

## Återställningsigenkänning {#rollback-detection}

För återställningsidentifiering kräver vissa användningsregler att klienten upprätthåller tillståndsinformation för att rättigheterna ska kunna verkställas. För att t.ex. framtvinga regler för användning av uppspelningsfönstret lagrar klienten det datum och den tidpunkt då användaren först började visa innehållet. Den här händelsen startar uppspelningsfönstrets start. För att på ett säkert sätt framtvinga uppspelningsfönstret måste servern se till att användaren inte säkerhetskopierar och återställer klientens tillstånd för att ta bort uppspelningsfönstrets starttid som lagrats på klienten. Servern gör detta genom att spåra värdet för klientens återställningsräknare.

För varje begäran hämtar servern räknarens värde genom att anropa `RequestMessageBase.getClientState()` för att hämta `ClientState` objektet och sedan anropa `ClientState.getCounter()` för att erhålla det aktuella värdet för klienttillståndsräknaren. Servern bör lagra det här värdet för varje klient (använd `MachineId.getUniqueId()` för att identifiera klienten som är associerad med återställningsräknarens värde) och sedan anropa `ClientState.incrementCounter()` för att öka räknarvärdet med ett. Om servern upptäcker att räknarvärdet är mindre än det senaste värdet som servern ser kan klienttillståndet ha återställts.

Mer information om hur du identifierar klienttillstånd för manipulering finns i API-referensdokumentationen `ClientState` .

## Konfigurationsdata för global server{#global-server-configuration-data}

Förutom den konfiguration som används av licensservern `HandlerConfiguration` lagrar konfigurationsinformation som kan skickas till klienten för att styra hur licenser upprätthålls. Detta görs genom att skapa en `ServerConfigData` klass och anropa `HandlerConfiguration.setServerConfigData()`. De här inställningarna gäller endast licenser som utfärdas av den här licensservern.

Toleransen för klocktillbakaspolning är en egenskap som kan ställas in av licensservern för att styra hur klienten verkställer licenser. Som standard kan användare ställa in datorklockan fyra timmar tillbaka utan att göra licenserna ogiltiga. Om en licensserveroperator vill använda en annan inställning kan det nya värdet anges i `ServerConfigData` klassen. När du ändrar värdet för någon av dessa inställningar måste du öka versionsnumret genom att anropa `setVersion()`. De nya värdena skickas endast till klienten om klientversionen är äldre än den aktuella `ServerConfigData` versionen.

## DRM-principfil för korsdomän {#crossdomain-drm-policy-file}

Om licensservern finns på en annan domän än SWF-filen för videouppspelning behövs en DRM-principfil ( [!DNL crossdomain.xml]) mellan domäner för att SWF-filen ska kunna begära licenser från en licensserver. En DRM-principfil för flera domäner representeras av en XML-fil som gör att servern kan ange att dess data och dokument är tillgängliga för SWF-filer som hanteras från andra domäner. Alla SWF-filer som hanteras från en domän som anges i licensserverns DRM-korsdomänprincipfil har behörighet att komma åt data eller resurser från den licensservern.

Adobe rekommenderar att utvecklare följer vedertagna standarder när de distribuerar korsdomänprincipfilen genom att endast tillåta betrodda domäner att komma åt licensservern och begränsa tillgången till licensunderkatalogen på webbservern.

Mer information om DRM-principfiler mellan domäner finns på följande platser:

* Webbplatsinställningar (DRM-principfiler)
* DRM-principfilsspecifikation för flera domäner: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)