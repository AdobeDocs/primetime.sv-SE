---
title: Användarmetadata
description: Användarmetadata
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Användarmetadata {#user-metadata}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## REST API-slutpunkter {#clientless-endpoints}

`<REGGIE_FQDN>`:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

`<SP_FQDN>`:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Beskrivning {#description}

Hämta metadata som MVPD delade om den autentiserade användaren.


| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>`/api/v1/tokens/usermetadata | Strömmande app</br></br>eller</br></br>Programmerartjänst | 1. begärande</br>2.  deviceId (obligatoriskt)</br>3.  device_info/X-Device-Info (obligatoriskt)</br>4.  deviceType</br>5.  deviceUser (utgått)</br>6.  appId (utgått) | GET | XML eller JSON som innehåller användarmetadata eller felinformation om det misslyckas. | 200 - lyckades<p>404 - Inga metadata hittades<p>412 - Ogiltig AuthN-token (t.ex. utgången token) |


| Indataparameter | Beskrivning |
| --- | --- |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |
| deviceId | Byte för enhets-ID. |
| device_info/<p>X-Device-Info | Information om direktuppspelningsenhet.</br></br> **Obs!** Detta kan skickas som en URL-parameter, men på grund av den här parameterns potentiella storlek och begränsningar i längden på en GET-URL, bör det skickas som X-Device-Info i http-huvudet. </br></br> Läs mer här: [Skicka information om enhet och anslutning](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | Enhetstypen (t.ex. Roku, PC).</br></br> Om den här parametern är korrekt angiven erbjuder ESM värden som är [uppdelad per enhetstyp](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) när du använder Klientlös, så att olika typer av analyser kan utföras för t.ex. Roku, AppleTV, Xbox osv.</br></br> Se [Fördelar med att använda parametern för enhetstyp utan klient i mätvärden för pass](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md) </br></br> **Obs!** The `device_info` ersätter den här parametern. |
| _deviceUser_ | Enhetens användaridentifierare.</br></br> **Obs!** Om den används `deviceUser` ska ha samma värden som i [Skapa registreringskod](/help/authentication/registration-code-request.md) begäran. |
| _appId_ | Program-ID/namn. </br></br> **Obs!** The `device_info` ersätter den här parametern. Om den används `appId` ska ha samma värden som i [Skapa registreringskod](/help/authentication/registration-code-request.md) begäran. |

>[!NOTE]
> 
>Användarmetadatainformation ska vara tillgänglig när autentiseringsflödet har slutförts, men kan uppdateras i auktoriseringsflödet beroende på MVPD och på metadatatypen.




## Exempelsvar {#sample-response}

Efter ett lyckat anrop kommer servern att svara med ett XML- (standard) eller JSON-objekt med en struktur som liknar den som visas nedan:


```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
              zip: ["12345", "34567"],
              maxRating: { 
                  "MPAA": "PG-13",
                  "VCHIP": "TV-Y", 
                  "URL": "http://exam.pl/e/manage/ratings"
                         },
              householdID: "3456",
              userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
              channelID: ["channel-1", "channel-2"]
              }
    }
```

I objektets rot finns det tre noder:

* *uppdaterad*: anger en UNIX-tidsstämpel som representerar den senaste gången metadata uppdaterades. Den här egenskapen ställs in från början av servern när metadata genereras under autentiseringsfasen. Efterföljande anrop (efter att metadata har uppdaterats) resulterar i en inkrementell tidsstämpel.
* *data*: innehåller de faktiska metadatavärdena.
* *krypterad*: en array med de krypterade egenskaperna. Om du vill dekryptera ett specifikt metadatavärde måste programmeraren utföra en Base64-avkodning på metadata och sedan tillämpa en RSA-dekryptering på resultatvärdet med hjälp av dess egen privata nyckel (Adobe krypterar metadata på servern med programmerarens offentliga certifikat).

Om ett fel inträffar returnerar servern ett XML- eller JSON-objekt som anger ett detaljerat felmeddelande.

Mer information finns i [Användarmetadata](/help/authentication/user-metadata-feature.md).

[Tillbaka till REST API-referens](/help/authentication/rest-api-reference.md)
