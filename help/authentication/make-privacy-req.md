---
title: Hur man gör en sekretessförfrågan
description: Hur man gör en sekretessförfrågan
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# Hur man gör en sekretessförfrågan {#howto-make-privacy-request}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Identifierare och namnutrymmen {#identifier-namespace}

När du skickar en begäran om åtkomst eller borttagning av sekretess måste kundprogrammet inkludera följande identifierare:

* **mvpdID** - Unik identifierare för MVPD.
* **userID** - Identifierar unikt användaren av en programmerarapp, men härstammar från MVPD. Se Förstå användar-ID:n i Programmeröversikten.
* **IMSOrgID** - Adobe Experience Cloud Identity Management serviceorganisations-ID, som unikt identifierar kunden i Adobe Experience Cloud


Kontrollera exemplet nedan:

```JSON
"userIDs": [{
     "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",  -----> "Dish" is the id of the MVPD
     "type":"unregistered",
     "value":"1234-5678-8765-4321" ----> "1234-5678-8765-4321" is the userId associated with the MVPD account
}]
```

>[!IMPORTANT]
>
>Användarna måste autentiseras för att kunna generera sekretessförfrågningar för Primetime-autentisering. Annars måste programmeraren hitta andra sätt att extrahera användar-ID:t för MVPD.

## Olika typer av förfrågningar {#req-type}

Primetime Authentication stöder begäranden om åtkomst och borttagning.

### Åtkomst {#access-req}

För en åtkomstbegäran:

vi skickar tillbaka en JSON-fil som innehåller en sammanfattning av det totala antalet autentiserings- och auktoriseringsbegäranden som skapats för den registrerade.
alla dessa händelser filtreras per kund.


**Begär exempel**

Du måste överföra en JSON-fil med Primetimes autentiseringsidentifierare som du skickar dataåtkomstbegäran för. Följande exempel visar hur en välformad JSON ser ut:

```JSON
{
    "companyContexts": [{
            "namespace": "imsOrgID",
            "value": "1234567890@AdobeOrg"
        }
    ],
    "users": [{
            "key": "John Dow",
            "action": ["access"],
            "userIDs": [{
                "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",
                "type":"unregistered",
                "value":"1234-5678-8765-4321"
             }]
         
        }
    ],
    
    "include":["primetimeAuthentication"],
    "regulation" : "ccpa"
}
```

**Svarsexempel**

```JSON
{
    "jobId": "d9a6b417-f619-4420-82a3-09f61fa8eff3",
    "requestId": "15765127177927284RX-739",
    "userKey": "John Dow",
    "action": "access",
    "status": "complete",
    "submittedBy": "564f7c9a-e0c8-4e74-99b8-20317ae1e235@techacct.adobe.com",
    "createdDate": "12/16/2019 04:11 PM GMT",
    "lastModifiedDate": "12/16/2019 04:15 PM GMT",
    "userIds": [
        {
            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
            "value": "1234-5678-8765-4321",
            "type": "unregistered",
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Primetime Authentication",
            "retryCount": 0,
            "processedDate": "12/16/2019 04:15 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "results": {
                    "userContexts": [
                        {
                            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
                            "namespaceId": 0,
                            "value": "1234-5678-8765-4321",
                            "type": "unregistered"
                        }
                    ],
                    "receiptData": {
                        "createdAt": "2019-12-16T16:15:23.4Z",
                        "message": "Data summary",
                        "numberOfAuthenticationSessions": "6",
                        "numberOfAuthorizationDecisions": "11"
                    }
                },
                "message": "Success"
            }
        }
    ],
    "downloadUrl": "https://va7gdprdevblob.blob.core.windows.net/va7gdprdevblobpublic/usa/4161962b9e8ef0027453d7cc02ecd93d/d9a6b417-f619-4420-82a3-09f61fa8eff3/d9a6b417-f619-4420-82a3-09f61fa8eff3.zip",
    "regulation": "ccpa"
}
```

### Ta bort {#delete-req}

Du måste överföra en JSON-fil med Primetime-autentiserings-ID:n som du skickar begäran om databorttagning för. Följande exempel visar hur en välformad JSON ser ut:

**Begär exempel**

```JSON
{
    "companyContexts": [{
            "namespace": "imsOrgID",
            "value": "1234567890@AdobeOrg"
        }
    ],
    "users": [{
            "key": "John Dow",
            "action": ["delete"],
            "userIDs": [{
                "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",
                "type":"unregistered",
                "value":"1234-5678-8765-4321"
             }]
         
        }
    ],
    
    "include":["primetimeAuthentication"],
    "regulation" : "ccpa"
}
```

**Svarsexempel**

För en Delete-begäran:

* vi delar bara ett kvitto på att data har tagits bort, inte en aggregerad fil med alla data som har tagits bort.
* det kvitto som ingår i svaret innehåller en sammanfattning av det totala antalet autentiserings- och auktoriseringstoken som har påträffats för den registrerade.

```JSON
{
    "jobId": "aab380d1-a0cd-4a0d-ba95-2649ee90c063",
    "requestId": "15759883098453100RX-074",
    "userKey": "John Dow",
    "action": "delete",
    "status": "complete",
    "submittedBy": "564f7c9a-e0c8-4e74-99b8-20317ae1e235@techacct.adobe.com",
    "createdDate": "12/10/2019 02:31 PM GMT",
    "lastModifiedDate": "12/10/2019 02:34 PM GMT",
    "userIds": [
        {
            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
            "value": "1234-5678-8765-4321",
            "type": "unregistered",
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Primetime Authentication",
            "retryCount": 0,
            "processedDate": "12/10/2019 02:34 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "results": {
                    "userContexts": [
                        {
                            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
                            "namespaceId": 0,
                            "value": "1234-5678-8765-4321",
                            "type": "unregistered"
                        }
                    ],
                    "receiptData": {
                        "createdAt": "2019-12-10T14:34:55.274Z",
                        "message": "Data summary",
                        "numberOfAuthenticationSessions": "2",
                        "numberOfAuthorizationDecisions": "3"
                    }
                },
                "message": "Success"
            }
        }
    ],
    "downloadUrl": "https://va7gdprdevblob.blob.core.windows.net/va7gdprdevblobpublic/usa/4161962b9e8ef0027453d7cc02ecd93d/aab380d1-a0cd-4a0d-ba95-2649ee90c063/aab380d1-a0cd-4a0d-ba95-2649ee90c063.zip",
    "regulation": "ccpa"
}
```

## Så här utlöser du en begäran {#trigger-req}

Det finns två sätt för kunder att skicka sekretessförfrågningar till Adobe:

* **manuellt** - genom att använda [Privacy Servicens användargränssnitt](#privacy-service-ui)
* **automatiskt** - genom att använda [Privacy Services-API ](#privacy-service-api)

### Genom att använda Privacy Servicens användargränssnitt {#privacy-service-ui}

A [komplett självstudiekurs](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) om hur du får åtkomst till och använder Privacy Servicens användargränssnitt finns online via Adobe I/O tjänster. Dessutom kan kunderna använda den här länken för att få tillgång till bibliotek med videoklipp och artiklar om sekretessbestämmelser. Klicka på Adobe Experience Cloud- och GDPR-menyn. Detta öppnar ett antal videofilmer -&quot;GDPR UI How-to&quot; förklarar hur du använder det.

I användargränssnittet måste kunderna läsa in sina egna IMSOrgID och en JSON som innehåller GDPR begär information för varje produkt.

### Genom att använda Privacy Services-API {#privacy-service-api}

Adobe Experience Platform Privacy Service erbjuder en gemensam, centraliserad lösning för begäran om åtkomst/radering och avanmälan av försäljningsförfrågningar för privata data.

The **Privacy Services-API-dokumentation** behandlar ingående hur en Adobe-kund kan integrera med Adobe API:t.

**Visualisera API-anrop med Postman (en kostnadsfri tredjepartsprogramvara):**

* [Privacy Service API Postman-samling på GitHub](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Privacy%20Service%20API.postman_collection.json)
* [Videoguide för att skapa Postman-miljön](https://video.tv.adobe.com/v/28832)
* [Steg för att importera miljöer och samlingar i Postman](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)


**API-sökvägar:**

* PLATFORM Gateway-URL: `https://platform.adobe.io/`
* Bassökväg för detta API: `/data/core/privacy/jobs`
* Exempel på en fullständig sökväg: `https://platform.adobe.io/data/core/privacy/jobs/ping`


**Obligatoriska rubriker:**

* Alla samtal kräver rubriker `Authorization`, `x-gw-ims-org-id`och `x-api-key`. Mer information om hur du hämtar dessa värden finns i **självstudiekurs om autentisering**.
* Alla begäranden med en nyttolast i begärandetexten (som anrop till POST, PUT och PATCH) måste innehålla rubriken `Content-Type` med värdet `application/json`.

<!--

>[!RELATEDINFORMATION]
>
>* [Privacy Services Overview](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md)
>* Privacy Service API documentation

-->