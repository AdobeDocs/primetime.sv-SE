---
seo-title: Information om policyarbetsflöde
title: Information om policyarbetsflöde
uuid: b355fcf6-3416-440f-9b30-a155e20f9f74
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---


# BEES-arbetsflöde {#bees-workflow}

**Sammanfattning:**

* **Policy**  - Skapa en BEES-kompatibel DRM-princip som anger att BEES krävs för allt innehåll som paketeras med den här principen.
* **Paketera**  - Paketera innehåll med den BEES-medvetna DRM-principen.
* **Autentisering**  - Autentisera din klientenhet och använd Primetimes DRM API, eller Primetime API, för att associera denna token med Primetime Cloud DRM. Om du gör det skickar klientenheten denna autentiseringstoken upp till Primetime Cloud DRM tillsammans med alla licensbegäranden. Primetime Cloud DRM kommer inte att bearbeta den här token, utan skickar den (som en ogenomskinlig blob) till BEES-slutpunkten för bearbetning.
* **Licensiering**  - Begär en licens för ditt skyddade innehåll. Klientenheten lägger automatiskt till din tidigare angivna autentiseringstoken till samtalet.
* **Tillstånd**  - Primetime Cloud DRM avgör att innehållet paketerades med en profil som requiresBEES. Primetime Cloud DRM skapar en JSON-begäran som skickas till BEES-slutpunkten. Svaret på BEES instruerar Primetime Cloud DRM om huruvida en licens ska utfärdas eller inte, och eventuellt vilken DRM-princip som ska användas.

## Information om policyarbetsflöde {#policy-workflow-details}

När Primetime Cloud DRM bearbetar en licensbegäran tolkas DRM-principen i begäran för att avgöra om ett anrop till en serverdelstjänst krävs innan innehållet kan visas. Om ett BEES-anrop *är* krävs skapar Primetime Cloud DRM BEES-begäran och tolkar sedan DRM-principen för att erhålla en angiven BEES URL-slutpunkt för BEES-begäran.

Använd DRM-principen som anger BEES-kravet och ange följande två anpassade egenskaper i profilen:

    *`policy.customProp.1=bees.required=&lt;true>`
    *`policy.customProp.2=bees.url=&lt;url to=&quot;&quot; your=&quot;&quot; BEES=&quot;&quot; endpoint=&quot;&quot;>`

<!--<a id="example_F617FC49A4824C0CB234C92E57D876D3"></a>-->

Om du till exempel använder principhanteraren för DRM-princip för Primetime ( [!DNL AdobePolicyManager.jar]) skulle du ange följande två anpassade egenskaper i konfigurationsfilen [!DNL flashaccesstools.properties]:

* `policy.customProp.1=bees.required=true`
* `policy.customProp.2=bees.url=https://mybeesserver.example.com/bees`

>[!NOTE]
>
>Om du redan använder `policy.customProp.1` eller `policy.customProp.2` för en annan egenskap använder du bara unika nummer för de nyare egenskaperna.

## Information om paketarbetsflöde {#package-workflow-details}

Under paketeringen av ditt Adobe Access-skyddade innehåll måste du tillämpa en av dina BEES-medvetna DRM-profiler på innehållet.

## Information om autentiseringsarbetsflöde {#authentication-workflow-details}

För att BEES-slutpunkten ska kunna fatta beslut om tillstånd måste klientenheten tillhandahålla autentiseringsinformation. Du uppnår detta genom att använda din egen kundspecifika autentiseringstoken.

Primetime Cloud DRM behöver inte förstå denna token, utan skickar bara denna token till din BEES-slutpunkt. Klientenheten ansvarar för att skapa eller hämta denna token och ställa in den med API:t `DRMManager.setAuthenticationToken()`.

Gör följande för att associera denna token med Primetime Cloud DRM så att den skickas med licensbegäran:

Instansiera `DRMManager`-objektet med DRM-metadata för innehållet som paketerades för Primetime Cloud DRM.

Metoden `setAuthenticationToken()` fungerar genom att associera den angivna bytearrayen med licensserverns URL som finns i DRM-metadata som användes för att instansiera `DRMManager`.

```java
//client device acquires auth token needed by your BEES endpoint  
DRMManager mgr = new DRMManager(<DRM Metadata of CloudDRM content>);  
mgr.setAuthenticationToken(<auth token>);
```

Token skickas med alla licensbegäranden tills token rensas genom att anropa `.setAuthenticationToken` med null som parameter.

## Information om licensarbetsflöde{#license-workflow-details}

Begär en licens från Primetime Cloud DRM genom att ringa `mgr.loadVoucher()`.

## Tillståndsbegäran och svarsinformation{#entitlement-request-and-response-details}

När Primetime Cloud DRM fastställer att innehållet har paketerats med en BEES-kompatibel DRM-princip skapas följande JSON-begäran som ska skickas till BEES-slutpunkten som anges i DRM-principen:

```
{
    "title":"Entitlement Request",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"Unique ID for this message. Used to confirm that the
                           returned response is for this particular message."
        },
        "version": {
            "type":"string",
            "description":"BEES Request Version. Currently 1."
        },
        "contentID": {
            "type":"string",
            "description":"Content ID (GUID)"
        },
        "customerSpecificAuthToken": {
            "type":"string",
            "description":"Base64-encoded authentication token. Must be set
                           explicitly by client before making the license request."
        }
    },
    "required": [
        "messageID",
        "version",
        "contentID"
    ]
}
```

Följande svar förväntas från BEES-slutpunkten:

```
{
    "title":"Entitlement Response",
    "type":"object",
    "properties": {
        "messageID": {
            "type":"string",
            "description":"ID of the Entitlement Request that this Response is
                           handling. Must exactly match the ID of the request
                           or this response will be rejected."
        },
        "version": {
            "type":"string",
            "description":"BEES Response Version. Currently 1."
        },
        "isAllowed": {
            "type":"boolean",
            "description":"Grant the license or not."
        },
        "policy": {
            "type":"string",
            "description":"Base64-encoded policy to enforce  If no policy is
                           provided, the policy that was packaged with the content
                           during packaging time will be used to generate the license."
        },
        "error": {
            "type":"integer",
            "description":"An error number produced by the entitlement server.
                           Will be passed to the client as the 'code' field of
                           the server error response."
        },
        "errorText": {
            "type":"string",
            "description":"Additional error information produced by the
                           entitlement server. Will be passed to the client as
                           the 'text' field of the server error response."
        }
    },
    "required": [
        "messageID",
        "version",
        "isAllowed"
    ]
}
```

Primetime Cloud DRM använder svaret för att avgöra om den ska utfärda en licens till den begärande enheten eller inte, och om den ska ersätta en ny DRM-princip i licensgenereringsprocessen. Om `isAllowed` är `true` och ingen princip anges i svaret, kommer den ursprungliga DRM-principen som användes under paketeringstiden att användas för att generera licensen.