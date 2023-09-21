---
title: MVPD-auktorisering
description: MVPD-auktorisering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# MVPD-auktorisering

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Ökning {#mvpd-authz-overview}

Auktorisering (AuthZ) utförs via bakåtkanalskommunikation (server-till-server) mellan en serverdelsserver som är värd för Adobe och MVPD AuthZ-slutpunkten.

För AuthZ-begäranden ska åtkomstslutpunkten kunna behandla minst följande parametrar:

* **Uid**. Det användar-ID som togs emot från autentiseringssteget.

* **Resurs-ID**. En sträng som identifierar en viss innehållsresurs. Resurs-ID anges av Programmeraren och MVPD måste förstärka affärsreglerna för dessa resurser (t.ex. genom att kontrollera att användaren prenumererar på en viss kanal).

Förutom att avgöra om användaren är behörig måste svaret innehålla en TTL-gräns (time-to-live) för auktorisationen, det vill säga när auktorisationen upphör att gälla. Om TTL inte anges misslyckas AuthZ-begäran.  Av denna anledning **TTL är en obligatorisk konfigurationsinställning på Adobe Primetime autentiseringssida**, för att täcka fallet när ett dokument för dokumentationsskydd inte inkluderar TTL i sin begäran.

## Begäran om auktorisering {#authz-req}

En AuthZ-begäran måste innehålla ett ämne för vars räkning begäran görs, de resurser som ämnet försöker få åtkomst till, den åtgärd som ämnet försöker utföra på resursen och den miljö där åtgärden ska utföras. När det gäller Adobe Primetime-autentisering motsvarar dessa element:

| XACML-element | Motsvarar |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Ämne | Det huvud som identifieras av den autentiserade sessionen, som refereras av attributvärdet för subject-token i SAML-försäkran. |
| Resurs | En URI för den skyddade resursen. |
| Åtgärd | VISA. |
| Miljö | Inkluderar IP-adressen för den begärande klienten, vilket visas av SP:n. |



SP:n måste förbereda en XACML Authorization DecisionQuery och skicka den (via HTTP-POST) till (tidigare överenskomna) Policy Decision Point (PDP) för IdP:n. Nedan visas ett exempel på en enkel XACML-begäran (se XACML-kärnspecifikation):

```XML
POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```


När AuthZ-begäran har tagits emot utvärderar MVPD-filens PDP begäran och avgör om ämnet ska kunna utföra den begärda åtgärden på resursen. MVPD returnerar sedan ett svar med ett beslut, en statuskod och ett meddelande enligt beskrivningen i behörighetssvaret nedan.

## Auktoriseringssvaret {#authz-response}

Svaret på AuthZ-begäran kommer efter det att MVPD utvärderat begäran och tillämpar de begärda affärsreglerna för att avgöra om ämnet får utföra den begärda åtgärden på resursen. Returnerat svar på Adobe Primetime-autentisering uttrycks igen efter XACML-kärnspecifikationen med ett beslut, en statuskod, ett meddelande och skyldigheter som SP har som PEP (Policy Enforcement Point). Här följer ett exempel på svar:

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

Nedan följer en lista över DENY-skyldigheter som Adobe Primetime-autentisering stöder och gör det möjligt för programmerare att uppfylla:

* **urn:tve:xacml:2.0:obligations:restrict-pc** - Prenumeranten har misslyckats med en föräldrakontroll och SP:n måste vidta lämpliga åtgärder för att begränsa åtkomsten till det här innehållet.

* **urn:tve:xacml:2.0:obligations:uppgradera** - Abonnenten har inte rätt abonnemangsnivå.  Prenumerationen måste uppgraderas för att du ska kunna få tillgång till innehållet.

Adobe Primetime-autentisering stöder följande **TILLÅT** Programmerarna har följande skyldigheter och kan fullgöra dem:

* **urn:cablelabs:loca:1.0:obligations:logg** - Adobe Pass loggar transaktionen och kan göra den tillgänglig via den överenskomna rapporteringsmekanismen.

* **urn:cablelabs:loca:1.0:obligations:reauthz** - Adobe Primetime-autentisering uppdaterar auktoriseringen igen om n sekunder (anges som ett argument till Skyldigheten via ett XACML AttributeAssignment - se XACML Core spec, avsnitt 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->
