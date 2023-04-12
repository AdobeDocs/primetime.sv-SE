---
title: Användarmetadata
description: Användarmetadata
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---


# Användarmetadata {#user-metadata}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## REST API-slutpunkter {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Beskrivning {#description}

Hämta metadata som MVPD delade om den autentiserade användaren.

<div>


| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/usermetadata | Strömmande app</br></br>eller</br></br>Programmerartjänst | 1. begärande</br>2.  deviceId (obligatoriskt)</br>3.  device_info/X-Device-Info (obligatoriskt)</br>4.  deviceType</br>5.  deviceUser (utgått)</br>6.  appId (utgått) | GET | XML eller JSON som innehåller användarmetadata eller felinformation om det misslyckas. | 200 - lyckades</br></br>404 - Inga metadata hittades</br></br>412 - Ogiltig AuthN-token (t.ex. utgången token) |


| Indataparameter | Beskrivning |
| --- | --- |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |
| deviceId | Byte för enhets-ID. |
| device_info/</br></br>X-Device-Info | Information om direktuppspelningsenhet.</br></br>**Anteckning**: Detta kan skickas som en URL-parameter för device_info, men på grund av parameterns potentiella storlek och begränsningar i längden på en GET-URL bör det skickas som X-Device-Info i http-huvudet. </br></br>Läs mer här: **Skicka information om enhet och anslutning** <!--http://tve.helpdocsonline.com/passing-device-information-->. |
| _deviceType_ | Enhetstypen (t.ex. Roku, PC).</br></br>Om den här parametern är korrekt angiven erbjuder ESM värden som är [uppdelad per enhetstyp](/help/authentication/entitlement-service-monitoring-overview.md#progr-filter-metrics) när du använder Klientlös, så att olika typer av analyser kan utföras för t.ex. Roku, AppleTV, Xbox osv.</br></br>Se [Fördelar med att använda parametern för enhetstyp utan klient i Pass etrics ](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**Obs!** The `device_info` ersätter den här parametern. </br> |
| _deviceUser_ | Enhetens användaridentifierare.</br></br>**Obs!**Om den används, `deviceUser` ska ha samma värden som i [Skapa registreringskod](/help/authentication/registration-code-request.md) begäran. |
| _appId_ | Program-ID/namn. </br></br>**Obs!**The `device_info` ersätter den här parametern. Om den används, `appId` ska ha samma värden som i **Skapa registreringskod** begäran. |

>[!NOTE]
> 
>Användarmetadatainformation ska vara tillgänglig när autentiseringsflödet har slutförts, men kan uppdateras i auktoriseringsflödet beroende på MVPD och på metadatatypen.

</br>

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
```

I objektets rot finns det tre noder:

* **uppdaterad**: anger en UNIX-tidsstämpel som representerar den senaste gången metadata uppdaterades. Den här egenskapen ställs in från början av servern när metadata genereras under autentiseringsfasen. Efterföljande anrop (efter att metadata har uppdaterats) resulterar i en inkrementell tidsstämpel.

* **data**: innehåller de faktiska metadatavärdena.

* **krypterad**: en array med de krypterade egenskaperna. Om du vill dekryptera ett specifikt metadatavärde måste programmeraren utföra en Base64-avkodning på metadata och sedan tillämpa en RSA-dekryptering på resultatvärdet med hjälp av dess egen privata nyckel (Adobe krypterar metadata på servern med programmerarens offentliga certifikat).

Om ett fel inträffar returnerar servern ett XML- eller JSON-objekt som anger ett detaljerat felmeddelande.

Mer information finns i [Användarmetadata](/help/authentication/user-metadata.md).

### [Tillbaka till REST API-referens](/help/authentication/rest-api-reference.md).
