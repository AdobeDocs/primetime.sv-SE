---
title: API-referens för JavaScript SDK
description: API-referens för JavaScript SDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---

# API-referens för JavaScript SDK {#javascript-sdk-api-reference}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## API-referens {#api-reference}

Dessa funktioner initierar förfrågningar om interaktion med ett MVPD. Alla anrop är asynkrona. Du måste implementera [återanrop](#callbacks) för att hantera svaren:

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logOut()](#logout)


## setRequestor (inRequestorID, endpoints, options){#setrequestor(inRequestorID,endpoints,options)}

**Beskrivning:** Identifierar webbplatsen som förfrågningarna kommer från.  Du måste ringa detta anrop innan du kan göra andra API-anrop i en kommunikationssession.

**Parametrar:**

- *inRequestorID* - Den unika identifierare som Adobe tilldelat den ursprungliga platsen under registreringen.

- *slutpunkter* - Den här parametern är valfri. Det kan vara något av följande värden:

   - En array som gör att du kan ange slutpunkter för autentisering och auktoriseringstjänster som tillhandahålls av Adobe (olika instanser kan användas i felsökningssyfte). Om flera URL:er anges består MVPD-listan av slutpunkterna från alla tjänsteleverantörer. Varje MVPD är kopplat till den snabbaste tjänsteleverantören, dvs. den leverantör som svarade först och som stöder det MVPD. Som standard (om inget värde anges) används Adobes tjänstleverantör (<http://sp.auth.adobe.com/>).

  Exempel:
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`

- *alternativ* - Ett JSON-objekt som innehåller programmets ID-värde, uppdateringslösa inställningar för Visitor ID-värde (inloggning i bakgrunden) och MVPD-inställningar (iFrame). Alla värden är valfria.
   1. Om detta anges rapporteras Experience Cloud visitorID för alla nätverksanrop som utförs av biblioteket. Värdet kan användas senare för avancerade analysrapporter.
   2. Om den unika identifieraren för programmet anges -`applicationId` - värdet läggs till i alla efterföljande anrop som görs av programmet som en del av HTTP-huvudet X-Device-Info. Värdet kan hämtas senare från [ESM](/help/authentication/entitlement-service-monitoring-overview.md) rapporter med rätt fråga.

  **Obs!** Alla JSON-tangenter är skiftlägeskänsliga.

  Exempel:

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- Programmeraren kan åsidosätta de MVPD-inställningar som har konfigurerats i Adobe Primetime-autentisering genom att ange om en iFrame krävs eller inte för inloggning (*iFrameRequired* och iFrame-måtten (*iFrameWidth* och *iFrameHeight* tangenter). JSON-objektet har följande mall:

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```


Alla tangenter på den översta nivån i mallen ovan är valfria och har standardvärden (*backgroundLogin*, *backgroundLogut*&#x200B;är false som standard och mvpdConfig är null, vilket innebär att inga MVPD-inställningar åsidosätts).


- **Anteckning**: Om du anger ogiltiga värden/typer för parametrarna ovan resulterar det i ett odefinierat beteende.



Här är ett exempel på konfiguration för följande scenario: aktivera uppdatering utan inloggning och inloggning, ändra MVPD1 till fullständig sidomdirigering (ej iFrame) och MVPD2 till iFrame-inloggning med width=500 och height=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**Återanrop utlösta:** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[Tillbaka till början](#top)

</br>

## getAuthorization(inResourceID, redirect_url) {#getauthorization(inresourceid,redirect_url)}

**Beskrivning:** Begär auktorisering för den angivna resursen. Varje gång en kund försöker få åtkomst till en auktoriserbar resurs anropar du den här funktionen för att få en kort åtkomsttoken från Access Enabler. Resurs-ID:n avtalas med det sidodokument som tillhandahåller auktorisering.

Använder den cachelagrade autentiseringstoken för den aktuella kunden. Om ingen sådan token hittas initierar autentiseringsprocessen först och fortsätter sedan med auktoriseringen.

**Parametrar:**

- `inResourceID` - ID:t för resursen som användaren begär auktorisering för.
- `redirect_url` - Du kan också ange en omdirigerings-URL så att MVPD:s auktoriseringsprocess återgår till den sidan i stället för den sida som auktoriseringen initierades från.


**Återanrop utlösta:** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) om framgång, [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) vid fel

>[!CAUTION]
>
>Använd checkAuthorization() i stället för getAuthorization() när det är möjligt. Metoden getAuthorization() startar ett fullständigt autentiseringsflöde (om användaren inte är autentiserad), vilket kan leda till en komplicerad implementering hos programmeraren.

</b>

[Tillbaka till början](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**Beskrivning:** Begär autentisering för den aktuella kunden. Anropas vanligtvis som svar på en klickning på en inloggningsknapp. Söker efter en cachelagrad autentiseringstoken för den aktuella kunden. Om ingen sådan token hittas initierar autentiseringsprocessen. Detta anropar standarddialogrutan eller den anpassade dialogrutan för val av leverantör och använder sedan den valda providern för att dirigera om till inloggningsgränssnittet för MVPD.

När det är klart skapar och sparar en autentiseringstoken för användaren. Om autentiseringen misslyckas returnerar providern ett felmeddelande till din [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) återanrop.

**Parametrar:**

- redirect_url - Ange en omdirigerings-URL om du vill, så att MVPD:s autentiseringsprocess returnerar användaren till den sidan i stället för till den sida som autentiseringen initierades från.

**Återanrop utlösta:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Tillbaka till början](#top)

</br>

## checkAuthN {#checkauthn}

**Beskrivning:** Kontrollerar den aktuella kundens autentiseringsstatus.  Inte associerat med något användargränssnitt.

**Återanrop utlösta:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[Tillbaka till början](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**Beskrivning:** Den här metoden används av programmet för att kontrollera auktoriseringsstatusen för den aktuella kunden och den angivna resursen. Det börjar med att kontrollera autentiseringsstatusen först. Om den inte autentiseras aktiveras callback-funktionen tokenRequestFailed() och metoden avslutas. Om användaren är autentiserad utlöses även auktoriseringsflödet. Se mer om [getAuthorization()](#getAuthZ-metod.

>[!TIP]
>
> **Använda check-status-funktioner**  Du behöver inte kontrollera status för autentisering eller auktorisering innan du begär auktorisering. Du kan anropa dessa funktioner för att till exempel uppdatera din egen statusvisning. Använd dem inte när du behöver göra något.

**Parametrar:**

- `inResourceID` - ID:t för resursen som användaren begär auktorisering för.


**Återanrop utlösta:**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**Beskrivning:** Begär preflight-auktoriseringsstatus för en lista med resurser.

**Parametrar:**

- *resurser*: Parametern resources är en array med resurser som auktoriseringen ska kontrolleras för. Varje element i listan ska vara en sträng som representerar resurs-ID:t. Resurs-ID har samma begränsningar som resurs-ID i `getAuthorization()` anrop, det vill säga, är ett avtalat värde mellan Programmer och MVPD, eller ett mediets RSS-fragment.

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

Denna API-variant är tillgänglig från och med JS SDK version 4.0


**Parametrar:**

- *resurser*: Parametern resources är en array med resurser som auktoriseringen ska kontrolleras för. Varje element i listan ska vara en sträng som representerar resurs-ID:t. Resurs-ID har samma begränsningar som resurs-ID i `getAuthorization()` anrop, det vill säga, är ett avtalat värde mellan Programmer och MVPD, eller ett mediets RSS-fragment.

- *cache*: Om det interna cacheminnet ska användas vid sökning efter förauktoriserade resurser. Det här är en valfri parameter som standard är **true**. Om värdet är true är beteendet identiskt med ovanstående API, vilket innebär att efterföljande anrop till den här funktionen kommer att använda ett internt cache-minne för att lösa en förauktoriserad resurs. Lösning **false** för den här parametern inaktiverar det interna cacheminnet, vilket resulterar i ett serveranrop varje gång **checkPreauthorizedResources** API anropas.

**Återanrop utlösta:** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)

</br>

[Tillbaka till början](#top)
</br>

## getMetadata(Key) {#getMetadata}

**Beskrivning:** Hämtar information som visas som metadata av biblioteket för Access Enabler.

Det finns två typer av metadata:

- **Statisk** (Autentiseringstoken TTL, auktoriseringstoken TTL och enhets-ID)
- **Användarmetadata** (Detta inkluderar användarspecifik information som skickas från MVPD till användarens enhet under autentiserings- och/eller auktoriseringsflödena)

**Mer information:** [Användarmetadata](#UserMetadata)

**Parametrar:**

- *key*: Ett ID som anger begärda metadata:
   - Om tangenten är `"TTL_AUTHN",` ställs frågan för att erhålla förfallotid för autentiseringstoken.

   - Om tangenten är `"TTL_AUTHZ"` och params är en array som innehåller resurs-ID:t som en sträng, görs frågan för att få fram förfallotiden för den auktoriseringstoken som är associerad med den angivna resursen.

   - Om tangenten är `"DEVICEID"` ställs frågan för att erhålla aktuellt enhets-ID. Observera att den här funktionen är inaktiverad som standard och programmerare bör kontakta Adobe för att få information om aktivering och avgifter.

   - Om nyckeln finns i följande lista över metadatatyper för användare, skickas ett JSON-objekt med motsvarande användarmetadata till [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) callback-funktion:

   - `"zip"` - Postnummer

   - `"encryptedZip"` - Krypterat postnummer

   - `"householdID"` - Hushållsidentifierare. Om ett MVPD inte stöder underkonton är detta identiskt med userID.

   - `"maxRating"` - Högsta föräldraklassificering för användaren

   - `"userID"` - användaridentifieraren. Om ett MVPD-dokument har stöd för underkonton och användaren inte är huvudkontot, kommer userID att vara ett annat än houseID.

   - `"channelID"` - Listan över kanaler som användaren har rätt att visa

   - `"is_hoh"` - Flagga som identifierar om en användare är chef för hushållet

   - `"encryptedZip"` - Krypterat postnummer

   - `"typeID"` - Flagga som identifierar om användarkontot är ett primärt/sekundärt konto

   - `"primaryOID"` - Hushållsidentifierare

   - `"postalCode"` - Liknar postnummer

   - `"acctID"` - Konto-ID

   - `"acctParentID"` - Överordnat konto-ID

  **Anteckning**: Vilka faktiska användarmetadata som är tillgängliga för en programmerare beror på vad ett separat programmeringsdokument (MVPD) erbjuder.  Se [Användarmetadata](#UserMetadata) för den aktuella listan över tillgängliga användarmetadata.


Till exempel:

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```


**Återanrop utlösta:** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[Tillbaka till början](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**Beskrivning:** Anropa den här funktionen när användaren har valt en MVPD i användargränssnittet för val av leverantör för att skicka leverantörens val till åtkomstfunktionen eller anropa den här funktionen med en null-parameter om användaren skulle ha avvisat användargränssnittet för val av leverantör utan att välja någon leverantör.

**Återanrop utlösta:**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[Tillbaka till början](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**Beskrivning:** Hämtar resultatet av kundens val i dialogrutan för val av leverantör. Detta kan användas när som helst efter den inledande autentiseringskontrollen.

Funktionen är asynkron och returnerar resultatet till `selectedProvider()` callback-funktion.

- **MVPD** Det aktuella MVPD-värdet, eller null om inget MVPD har valts.
- **AE_State** Resultatet av autentiseringen för den aktuella kunden av &quot;Ny användare&quot;, &quot;Användare ej autentiserad&quot; eller &quot;Användarautentiserad&quot;

**Återanrop utlösta:** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[Tillbaka till början](#top)

</br>

## utloggning {#logout}

**Beskrivning:** Loggar ut den aktuella kunden och rensar all autentiserings- och auktoriseringsinformation för den användaren. Tar bort alla authN- och authZ-tokens från kundens system.

**Återanrop utlösta:** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br>

[Tillbaka till början](#top)

</br>

## Återanropsdefinition {#calllback-definitions}

Du måste implementera dessa återanrop för att kunna hantera svaren på dina asynkrona förfrågningsanrop:

- [entitlementLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## entitlementLoaded() {#entitlementLoaded}

**Beskrivning:** Utlöses när åtkomstaktiveraren har slutfört initieringen och är redo att ta emot begäranden. Implementera den här återanropet för att veta när du kan starta kommunikationen med API:t för åtkomstaktivering.
</br>

[Tillbaka till början](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**Beskrivning:** Implementera det här återanropet för att ta emot konfigurationsinformationen och MVPD-listan.

**Parametrar:**

- *configXML*: xml-objekt som innehåller konfigurationen för den aktuella REQUESTOR inklusive MVPD-listan.


**Utlöses av:** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[Tillbaka till början](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**Beskrivning:** Implementera det här återanropet för att anropa ditt eget anpassade användargränssnitt för val av leverantör. Dialogrutan ska ha visningsnamnet (och den valfria logotypen) för att ge kunderna möjlighet att välja. När kunden har gjort ett val och avvisat dialogrutan skickar du det associerade ID:t för den valda leverantören i samtalet till *setSelectedProvider()*.

**Parametrar:**

- *leverantörer* - En array med objekt som representerar de begärda PDF-filerna:

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**Utlöses av:** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[Tillbaka till början](#top)

</br>

## createIFrame(inWidth, inHeight) {#createIFrame(inWidth,inHeight)}

**Beskrivning:** Implementera det här återanropet om användaren har valt ett MVPD som kräver en iFrame där användargränssnittet för inloggningssidan för autentisering ska visas.

**Utlöses av:**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [Tillbaka till början](#top)

</br>

## setAuthenticationStatus(isAuthenticated, errorCode) {#set-authn-status-isauthn-error}

**Beskrivning:** Implementera det här återanropet för att ta emot autentiseringsstatusen (1=autentiserad eller 0=inte autentiserad) och ett beskrivande felmeddelande om något fel uppstod vid försök att fastställa autentiseringsstatusen (tom sträng när kontrollen har slutförts).

>[!NOTE]
> 
>Om du använder den aktuella [Avancerad felrapportering](/help/authentication/error-reporting.md) kan du ignorera parametern errorCode som skickas till den här funktionen.  Flaggan isAuthenticated används dock fortfarande för att spåra autentiseringsstatusen för en användare i berättigandeflödet


**Parametrar:**

- *isAuthenticated* - Tillhandahåller autentiseringsstatus: 1 (autentiserad) eller 0 (inte autentiserad).
- *errorCode* - Alla fel som uppstod när autentiseringsstatusen fastställdes. En tom sträng om ingen.


**Utlöses av:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[Tillbaka till början](#top)

</br>

## sendTrackingData(trackingEventType, trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>Enhetstypen och operativsystemet härleds genom användning av ett offentligt Java-bibliotek (<http://java.net/projects/user-agent-utils>) och användaragentsträngen. Observera att denna information endast tillhandahålls som ett grovt sätt att dela upp mätvärden för drift i enhetskategorier, men att Adobe inte kan ta något ansvar för felaktiga resultat. Använd den nya funktionen i enlighet med detta.

**Beskrivning:** Implementera det här återanropet för att ta emot spårningsdata när specifika händelser inträffar. Du kan till exempel använda detta för att hålla reda på hur många användare som har loggat in med samma inloggningsuppgifter. Spårning kan för närvarande inte konfigureras. Med Adobe Primetime-autentisering 1.6 `sendTrackingData()` rapporterar även information om enheten, Access Enabler-klienten och operativsystemstypen. The `sendTrackingData()` callback-funktionen är fortfarande bakåtkompatibel.

- Möjliga värden för enhetstypen:
   - dator
   - surfplatta
   - mobil
   - gameconsole
   - okänd

- Möjliga värden för klienttypen Åtkomstaktivering:
   - html5
   - ios
   - android


Skickar händelsetypen och en array med associerad information. Händelsetyper är:

| mvpdSelection | Användaren valde ett MVPD-dokument i en dialogruta där han/hon valde leverantör. |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | En verifieringskontroll har slutförts. |
| permissionDetection | En auktoriseringsbegäran har slutförts. |

</br>
Data är specifika för varje händelsetyp:
</br>

| Händelsetyp (String) | Data (matris) |
|:--- | :--- |
| mvpdSelection | 0: Markerat MVPD |
|  | 1: Enhetstyp |
|  | 2: Klienttyp för åtkomstaktivering |
|  | 3: OS |
| authenticationDetection | 0: Anger om tokenbegäran lyckades (true/false) |
|  | 1: MVPD ID |
|  | 2: GUID |
|  | 3: Token finns redan i cache (true/false) |
|  | 4: Enhetstyp |
|  | 5: Klienttyp för åtkomstaktivering |
|  | 6: OS |
| permissionDetection | 0: Anger om tokenbegäran lyckades (true/false) |
|  | 1: MVPD ID |
|  | 2: GUID |
|  | 3: Token finns redan i cache (true/false) |
|  | 4: Fel |
|  | 5: Information |
|  | 6: Enhetstyp |
|  | 7: Klienttyp för åtkomstaktivering |
|  | 8: OS |


**Utlöses av:** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[Tillbaka till början](#top)

</br>

## setToken(inRequestedResourceID, inToken) {#setToken(inRequestedResourceID,inToken)}

**Beskrivning:** Implementera det här återanropet för att ta emot den kortlivade medietoken (inToken) och ID:t för resursen (inRequestedResourceID) som en auktoriseringsbegäran eller en kontrollauktoriseringsbegäran gjordes för och har slutförts.

**Utlöses av:** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[Tillbaka till början](#top)

</br>

## tokenRequestFailed(inRequestedResourceID, inRequestErrorCode, inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**Beskrivning:** Implementera det här återanropet som ska signaleras när en auktorisering eller en begäran om kontrollauktorisering har misslyckats. Kan även användas av en MVPD för att ge ett anpassat meddelande som ska visas av programmeraren.

>[!IMPORTANT]
>
>Den här återanropsfunktionen är en del av det äldre, ursprungliga felrapporteringssystemet för autentisering i Primetime. Den bevaras för bakåtkompatibilitet, men den här funktionen behöver inte användas alls om du har implementerat dina egna återanrop med det aktuella avancerade felrapporteringssystemet. Det nyare felrapporteringssystemet ger mer detaljerad information om varför en auktorisering (eller annan åtgärd) misslyckades, tillsammans med förslag på åtgärder för varje typ av fel eller varning.

**Parametrar:**

- *inRequestedResourceID* - En sträng som anger det resurs-ID som användes i auktoriseringsbegäran.
- *inRequestErrorCode* - En sträng som visar felkoden för Adobe Primetime-autentisering och anger orsaken till felet. Möjliga värden är &quot;User Not Authenticated Error&quot; och &quot;User Not Authorized Error&quot;. Mer information finns i &quot;Callback error codes&quot; nedan.
- *inRequestDetailedErrorMessage* - En extra beskrivande sträng som är lämplig för visning. Om den här beskrivande strängen inte är tillgänglig av någon anledning skickar Adobe Primetime-autentiseringen en tom sträng **(&quot;&quot;)**.  Detta kan användas av en MVPD för att skicka anpassade felmeddelanden eller försäljningsrelaterade meddelanden. Om en prenumerant nekas auktorisering för en resurs, kan den kostnadsfria PDF-filen svara med en `*inRequestDetailedErrorMessage*` t.ex. **&quot;Du har för närvarande inte tillgång till den här kanalen i ditt paket. Om du vill uppgradera ditt paket klickar du \*här\*.&quot;** Meddelandet skickas med Adobe Primetime-autentisering via det här återanropet till programmerarens webbplats. Programmeraren kan sedan välja att visa eller ignorera den. Adobe Primetime-autentisering kan även använda `*inRequestDetailedErrorMessage*` för att meddela programmeraren om det tillstånd som kan ha orsakat ett fel. Till exempel: **&quot;Ett nätverksfel uppstod vid kommunikation med leverantörens auktoriseringstjänst.&quot;**



**Utlöses av:**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[Tillbaka till början](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**Beskrivning:** Återanrop utlöses av Access Enabler som levererar listan över auktoriserade resurser som returneras efter ett anrop till `checkPreauthorizedResources()`.

**Parametrar:**

- *authorizedResources*: Listan över auktoriserade resurser.

**Utlöses av:** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[Tillbaka till början](#top)

</br>

## setMetadataStatus(nyckel, krypterad, data) {#setMetadataStatus(key,encrypted,data)}

**Beskrivning:** Återanrop utlöses av Access Enabler som levererar de metadata som efterfrågas via en `getMetadata()` ring.

**Mer information:** [Användarmetadata](#userMetadata)

**Parametrar:**

- *key (String)*: Nyckeln till de metadata som begäran gjordes för.
- *encrypted (Boolean)*: En flagga som anger om värdet är krypterat eller inte. Om värdet är &quot;true&quot; är &quot;value&quot; en JSON Web Encrypted-representation av det faktiska värdet.
- *data (JSON-objekt)*: Ett JSON-objekt med representation av metadata.För enkla begäranden (&#39;`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;), result is a String (representing the Authentication TTL, Authorization TTL or Device ID). Om det gäller en begäran om användarmetadata kan resultatet vara ett primitivt eller JSON-objekt som representerar metadatanyttolasten. Den faktiska strukturen för JSON-användarmetadataobjekt liknar följande:

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```


Till exempel:

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```


**Utlöses av:** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[Tillbaka till början](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**Beskrivning:** Implementera det här återanropet för att ta emot den aktuella MVPD-filen och resultatet av autentiseringen av den aktuella användaren som är inkapslad i `result` parameter. The `result` parametern är ett objekt med följande egenskaper:

- **MVPD** Det aktuella MVPD-värdet, eller null om inget MVPD har valts.
- **AE\_State** Resultatet av autentiseringen för den aktuella användaren, antingen Ny användare, Användare ej autentiserad eller Användare autentiserad

**Utlöses av:** [getSelectedProvider()](#getSelProv)

</br>

[Tillbaka till början](#top)

</br>

### Felkoder för återanrop {#callback-error-codes}

| Allmänna fel | |
|:--- | :--- | 
| Internt fel | Ett systemfel uppstod vid försök att bearbeta begäran. |
| Fel: Providern är inte vald | Inträffar när kunden avbryter i dialogrutan för val av leverantör |
| Providern är inte tillgänglig | Inträffar när inga providers är tillgängliga. |

| Autentiseringsfel | |
|:--- | :--- | 
| Allmänt autentiseringsfel | Returneras när orsaken inte är känd eller inte kan publiceras. |
| Internt autentiseringsfel | Ett systemfel uppstod vid försök att autentisera. |
| Användaren är inte autentiserad | Användaren är inte autentiserad. |
| Fel: Flera autentiseringsbegäranden | Ytterligare autentiseringsbegäranden togs emot innan det första slutfördes. |

| Auktoriseringsfel | |
|:--- | :--- | 
| Allmänt auktoriseringsfel | Returneras när orsaken inte är känd eller inte kan publiceras. |
| Internt auktoriseringsfel | Ett systemfel uppstod vid försök att auktorisera. |
| Användaren är inte auktoriserad | Kunden har inte behörighet att visa det begärda innehållet. |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[Tillbaka till början](#top)
