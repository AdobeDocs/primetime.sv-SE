---
title: Returregistreringspost
description: Returregistreringspost
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Returregistreringspost {#return-registration-record}

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

Returnerar registreringskodposten som innehåller registreringskoden UUID, registreringskoden och det hash-kodade enhets-ID:t. 

 

<div>


| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestId}/regcode/{registrationCode}</br></br>Till exempel:</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJJCFK?format=xml | Strömmande app</br></br>eller</br></br>Programmerartjänst | 1. begärande  </br>    (Bankomponent)</br>2.  registreringskod  </br>    (Bankomponent) | GET | XML eller JSON som innehåller en registreringskod och information. Se schema och exempel nedan. | 200 |

{style=&quot;table-layout:auto&quot;}

</br>

| Indataparameter | Beskrivning |
| --- | --- |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |
| registreringskod | Registreringskodvärdet som skulle visas på direktuppspelningsenheten (anges i autentiseringsflödet). |

</br>

## XML-schema för svar {#response-xml-schema}

### Registreringskod XSD

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>
```

| Elementnamn | Beskrivning |
| --- | --- |
| id | UUID genererat av registreringskodstjänsten |
| kod | Registreringskod som genererats av registreringskodstjänsten |
| begärande | Begärande-ID |
| mvpd | MVPD-ID |
| genererad | Tidsstämpel för att skapa registreringskod (i millisekunder sedan 1 januari 1970 GMT) |
| förfaller | Tidsstämpel när registreringskoden upphör att gälla (i millisekunder sedan 1 januari 1970 GMT) |
| deviceId | Unikt enhets-ID (eller XSTS-token) |
| deviceType | Enhetstyp |
| deviceUser | Användaren är inloggad på enheten |
| appId | Program-ID |
| appVersion | Programversion |
| registrationURL | URL till inloggningswebbappen som ska visas för slutanvändaren |

{style=&quot;table-layout:auto&quot;}

### Exempelsvar {#sample-response}

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```

[Tillbaka till REST API-referens](http://tve.helpdocsonline.com/rest-api-reference)