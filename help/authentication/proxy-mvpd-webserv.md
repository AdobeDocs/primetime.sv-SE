---
title: Proxy MVPD-webbtjänst
description: Proxy MVPD-webbtjänst
exl-id: f75cbc4d-4132-4ce8-a81c-1561a69d1d3a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# Proxy MVPD-webbtjänst {#proxy-mvpd-wbservice}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Översikt {#overview-proxy-mvpd-webserv}

Ett MVPD-program för proxy är ett MVPD-program som förutom att hantera sin egen integrering med Adobe Primetime-autentisering även hanterar tillståndsprocessen för en grupp av associerade &quot;Proxied MVPDs&quot;. Detta är öppet för programmerare.

För att implementera ProxyMVPD-funktionen tillhandahåller Adobe Primetime-autentisering RESTful-webbtjänster som ProxyMVPD kan använda för att skicka och hämta listor över ProxiedMVPD. Protokollet som används för detta offentliga API är REST HTTP, med följande antaganden:

* Proxy MVPD använder HTTP GET-metoden för att hämta listan över de aktuella integrerade programmeringsgränssnitten.
* Proxy MVPD använder HTTP-POST-metoden för att uppdatera listan över de MVPD som stöds.

## Proxy MVPD-tjänster {#proxy-mvpd-services}

* [Hämta proxibla MVPD-filer](#retriev-proxied-mvpds)
* [Skicka proxygenererade MVPD-filer](#submit-proxied-mvpds)

### Hämta proxibla MVPD-filer {#retriev-proxied-mvpds}

Hämtar den aktuella listan över Proxied MVPD för ProxyMVPD som identifieras av apikey-parametern.

| Slutpunkt | Anropat av | Begäranrubriker | HTTP-metod | HTTP-svar |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey (obligatoriskt) | GET | <ul><li> 200 (ok) - Begäran har bearbetats och svaret innehåller en lista med ProxiedMVPD:er i XML-format</li><li>401 (obehörig) - Användarautentisering krävs eller auktorisering beviljas inte för angivna autentiseringsuppgifter.  Anger något av följande:<ul><li>Apikey-token finns inte i begärandehuvudet</li><li>Begäran kommer från en IP-adress som inte finns i tillåtelselista</li><li>Ogiltig token</li></ul></li><li>403 (ej tillåtet) - Anger antingen att åtgärden inte stöds för de angivna parametrarna, eller att proxy-MVPD inte har angetts som proxy eller saknas</li><li>405 (metod tillåts inte) - En annan HTTP-metod än GET eller POST användes. Antingen stöds inte HTTP-metoden generellt eller så stöds den inte för den här specifika slutpunkten.</li><li>500 (internt serverfel) - Ett fel uppstod på serversidan under förfrågningsprocessen.</li></ul> |

Exempel:

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`


Exempel på XML-svar:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```

### Skicka proxygenererade MVPD-filer {#submit-proxied-mvpds}

Flyttar en array med MVPD-filer som är integrerade med det MVPD-program som identifieras av apikey-parametern.

| Slutpunkt | Anropat av | Begäranrubriker | HTTP-metod | HTTP-svar |
|:------------------------------:|:---------:|:--------------------------------------------:|:-----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey (obligatoriskt) proxied-mvpds (obligatoriskt) | POST | <ul><li>201 (skapad) - push-åtgärden bearbetades</li><li>400 (felaktig begäran) - Servern kan inte behandla begäran:<ul><li>Inkommande XML följer inte schemat som publicerats i den här specifikationen</li><li>De proxibla mvpds har inga unika ID:n</li><li>BegärandeID:n som skickas finns inte för någon annan serverbehållarorsak för 400 svarskod</li></ul><li>401 (obehörig) - apikey är inte giltigt eller så är anroparens IP inte på tillåtelselista</li><li>403 (ej tillåtet) - Anger antingen att åtgärden inte stöds för de angivna parametrarna, eller att proxy-MVPD inte har angetts som proxy eller saknas</li><li>405 (metod tillåts inte) - En annan HTTP-metod än GET eller POST användes. Antingen stöds inte HTTP-metoden generellt eller så stöds den inte för den här specifika slutpunkten.</li><li>500 (internt serverfel) - Ett fel uppstod på serversidan under förfrågningsprocessen.</li></ul> |

Exempel:

`curl -X POST -H "apikey: <API_KEY>" "https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds" -d "proxied-mvpds=%3CproxiedMvpds%3E%3CproxiedMvpd%3E%3CdisplayName%3EFirst%20MVPD%20Name%3C%2FdisplayName%3E%3Cid%3EfirstMVPDId%3C%2Fid%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3C%2FproxiedMvpd%3E%3CproxiedMvpd%3E%3Cid%20ProviderID%3D%22ProviderID_Value_Sent_On_IdPEntry%22%3EmvpdPickerId%3C%2Fid%3E%3CdisplayName%3EMVPD%20Name%20Two%3C%2FdisplayName%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3CrequestorIds%3E%3CrequestorId%3ETHE_REQUESTOR_ID%3C%2FrequestorId%3E%3C%2FrequestorIds%3E%3C%2FproxiedMvpd%3E%3C%2FproxiedMvpds%3E"`



XML-exempel:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```


### Bokföringsfrekvens {#posting-frequency}

Adobe Primetime-autentisering rekommenderar att ProxyMVPD bara skickar sin lista över ProxiedMVPD när det finns en ändring från den tidigare push-funktionen.

### Tar bort proxiderade MVPD-filer {#delete-proxied-freqency}

Om ProxyMVPD överför en XML-post med en tom ProxiedMVPD-lista kommer den tomma listan att lagras i vårt system precis som alla andra listor, vilket innebär att den föregående listan tas bort.



## XSD-format {#xsd-format}

Adobe har definierat följande godkända format för publicering/hämtning av proxiderade MVPD från/till vår offentliga webbtjänst:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:pxm="http://tve.adobe.com/data/proxiedmvpd"
           targetNamespace="http://tve.adobe.com/data/proxiedmvpd"
           elementFormDefault="qualified"
           version="1.0">
    <xs:complexType name="iframeSize">
        <xs:all>
            <xs:element name="iframeHeight" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeWidth" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
        </xs:all>
    </xs:complexType>
    <xs:complexType name="requestorIds">
        <xs:annotation>
            <xs:documentation>List of requestors/programmers integrated with the proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:sequence>
            <xs:element name="requestorId" type="xs:string" minOccurs="1" maxOccurs="unbounded" nillable="false">
                <xs:annotation>
                    <xs:documentation>The requestor/programmer identifier recognized by Adobe</xs:documentation>
                </xs:annotation>
            </xs:element>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="proxiedMvpd">
        <xs:all>
            <xs:element name="id" minOccurs="1" maxOccurs="1" nillable="false">
                <xs:annotation>
                    <xs:documentation>The id must conform to the regular expression: ([a-zA-Z0-9]+((\-)|[_])*)</xs:documentation>
                </xs:annotation>
                <xs:complexType>
                    <xs:simpleContent>
                        <xs:extension base="xs:string">
                            <xs:attribute name="ProviderID">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="1"/>
                                        <xs:maxLength value="128"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:attribute>
                        </xs:extension>
                    </xs:simpleContent>
                </xs:complexType>
            </xs:element>
            <xs:element name="displayName" type="xs:string" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="logoURL" type="xs:anyURI" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeSize" type="pxm:iframeSize" minOccurs="0" maxOccurs="1"/>
            <xs:element name="requestorIds" type="pxm:requestorIds" minOccurs="0" maxOccurs="1"/>
        </xs:all>
    </xs:complexType>
    <xs:element name="proxiedMvpds">
        <xs:annotation>
            <xs:documentation>List of Proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:element name="proxiedMvpd" type="pxm:proxiedMvpd" minOccurs="0" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**Kommentarer om element:**

* `id` (obligatoriskt) - Det Proxierade MVPD-ID:t måste vara en sträng som är relevant för namnet på MVPD och som använder något av följande tecken (eftersom det kommer att visas för programmerare för spårningsändamål):
   * Alfanumeriska tecken, understreck (&quot;_&quot;) och bindestreck (&quot;-&quot;).
   * ID:t måste överensstämma med följande reguljära uttryck:
      `(a-zA-Z0-9((-)|_)*)`

      Det måste alltså ha minst ett tecken, börja med en bokstav och fortsätta med en bokstav, siffra, bindestreck eller understreck.

* `iframeSize` (valfritt) - Elementet iframeSize är valfritt och definierar storleken på iFrame om MVPD-autentiseringssidan ska finnas i en iFrame. Annars, om iframeSize-elementet inte finns, sker autentiseringen på en omdirigeringssida i en fullständig webbläsare.
* `requestorIds` (valfritt) - Värdet för requestIds anges av Adobe. Ett krav är att ett proxiderat MVPD ska integreras med minst ett RequestId. Om taggen &quot;requestIds&quot; inte finns i det proxiderade MVPD-elementet, kommer det proxierade MVPD att integreras med alla tillgängliga beställare som är integrerade under det proxybaserade MVPD-elementet.
* `ProviderID` (valfritt) - När attributet ProviderID finns i elementet id skickas värdet för ProviderID på SAML-autentiseringsbegäran till Proxy MVPD som Proxied MVPD/SubMVPD ID (i stället för id-värdet). I det här fallet används värdet för id endast i den MVPD-väljare som presenteras på Programmer-sidan och internt av Adobe Primetime-autentisering. Längden på ProviderID-attributet måste vara mellan 1 och 128 tecken.

## Säkerhet {#security}

För att en begäran ska anses giltig måste den uppfylla följande regler:

* Begäranhuvudet måste innehålla säkerhetsparametern apikey. (Detta är en programnyckel som unikt identifierar Proxy MVPD-anropen.)
* Begäran måste komma från en specifik IP-adress som är tillåten.
* Begäran måste skickas via SSL-protokollet.

Adobe anger tokens (statiska) värde. Det här värdet används i autentiserings- och auktoriseringsprocessen.  Alla parametrar i begärandehuvudet som inte finns med i listan ovan kommer att ignoreras.

Exempel:

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## Proxy MVPD-webbtjänstslutpunkter för Adobe Primetime autentiseringsmiljöer {#proxy-mvpd-wevserv-endpoints}

* **Produktions-URL:** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **Mellanlagrings-URL:** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **PreQual-Production URL:** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **URL för preQual-Staging:** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
