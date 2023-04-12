---
title: Fördelar med att använda parametern deviceType utan klient i autentiseringsmåtten Primetime
description: Fördelar med att använda parametern deviceType utan klient i autentiseringsmåtten Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Fördelar med att använda parametern deviceType utan klient i autentiseringsmåtten Primetime {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>

## Kontext

Parametern är valfri `deviceType` från det klientlösa API:t används i autentiseringsmått för Primetime som exponeras via [Tillståndsövervakning](/help/authentication/entitlement-service-monitoring-overview.md).

Tänk på att anslutningen mellan `deviceType` parameter och dess **fördelar** om autentiseringsmått för Primetime inte nämndes ursprungligen, är omfattningen av den här tekniska kommentaren att lägga till mer information om dem.

## Förklaring

The `deviceType` -parametern fanns i det klientlösa API:t sedan den första versionen, men dess konsekvenser för autentiseringsmåtten Primetime lades till i en senare version.



>[!IMPORTANT]
>
>Om parametern `deviceType` är korrekt inställd har den följande **förmån** i Entitlement Service Monitoring: erbjuder mätvärden som [uppdelad per enhetstyp](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) när du använder Klientlös, så att olika typer av analyser kan utföras för t.ex. Roku, AppleTV, Xbox osv.


Mer information om API:t för övervakning av berättigandetjänster finns i [detaljträd,](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) som illustrerar [dimensioner](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) (resurser) i ESM 2.0.

>[!NOTE]
>
>Innehållet i den här tekniska kommentaren lades också till i [Klientlöst API](#clientless_device_type).




## Implementering

Det finns två typer av [Klientlösa API:er](#web_srvs_summary) som används och som måste ha rätt `deviceType` set:

1. API:er som har `regcode` som en obligatorisk parameter och använder `deviceType` parameter som angavs när `regcode`, med följande API-anrop:
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestId}/regcode](#reg_serv)

1. API:er som har `deviceType` som en valfri parameter:
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorized](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorized](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/utloggning](#init_logout)

Vi rekommenderar att du använder `deviceType` och skicka korrekt klientlös enhetstyp för alla API:er.


