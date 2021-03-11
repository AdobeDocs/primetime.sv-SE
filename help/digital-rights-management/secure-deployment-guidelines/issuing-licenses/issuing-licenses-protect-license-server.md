---
description: 'Ni måste se till att ni på ett säkert sätt utfärdar licenser. Tänk på följande när det gäller att skydda licensservern '
title: Skydda licensservern
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---


# Skydda licensservern {#protecting-the-license-server}

Ni måste se till att ni på ett säkert sätt utfärdar licenser. Använd följande metoder för att skydda licensservern:

## Använder lokalt genererade listor över återkallade certifikat {#consuming-locally-generated-crls}

Använd Adobe Primetime DRM API:er för att verifiera signaturen om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL:er) och principuppdateringslistor.

Följande API:er kontrollerar att listorna inte har manipulerats och att listorna har signerats av rätt licensserver:

* Anropa [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) för att kontrollera signaturen innan du anger [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) till någon API.

   Mer information finns i [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Anropa [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) för att kontrollera signaturen innan du skickar `PolicyUpdateList` till någon API.

   Mer information finns i [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Använda listor över återkallade certifikat som publicerats av Adobe{#consuming-crls-published-by-adobe}

SDK hämtar regelbundet listor över återkallade certifikat som publiceras av Adobe. Du måste se till att åtkomsten till de här filerna inte blockeras eller att kontrollen av dessa listor över återkallade certifikat inte förhindras.

SDK har ett konfigurationsalternativ som ignorerar fel när du hämtar Adobe-CRL:er, och du kan bara använda det här alternativet i utvecklingsmiljöer. I produktionsmiljöer måste licensservern hämta CRL:er från Adobe. Om licensservern inte kan hämta en giltig CRL har ett fel uppstått.

## Genererar listor över återkallade certifikat som kompletterar dem som publicerats av Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Du kan använda Adobe Primetime DRM för att skapa listor över återkallade certifikat som kompletterar den lista över återkallade certifikat som publiceras av Adobe.

Primetimes DRM SDK kontrollerar och verkställer Adobe CRL:er. Du kan dock inte tillåta ytterligare klientdatorer genom att skapa en CRL som återkallar ytterligare datorautentiseringsuppgifter genom att skicka CRL:en till Primetime DRM SDK. När du utfärdar en licens kontrollerar SDK Adobe CRL och din CRL.

Information om hur du skapar CRL:er finns i [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Återställningsidentifiering {#rollback-detection}

Om din implementering av Adobe Primetime DRM använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som Tillåt listning.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om din implementering av Primetime DRM inte kräver återställningsräknaren kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som hämtas med [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) och det aktuella räknarvärdet i en databas.

Mer information om hur du ökar och spårar återställningsräknaren finns i [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) och Återställningsidentifiering.

## Antal datorer när licenser utfärdas {#machine-count-when-issuing-licenses}

Om affärsreglerna kräver att antalet datorer för en användare spåras, måste licensservern eller domänservern lagra de dator-ID som är associerade med användaren.

Det mest robusta sättet att spåra dator-ID:n är att lagra värdet som returneras av metoden [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) i en databas. När en ny begäran tas emot kan du jämföra dator-ID:t i begäran med kända dator-ID:n med [MachineId.match()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.match()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) utför en jämförelse av ID:n för att avgöra om ID:n representerar samma dator. Jämförelsen är bara praktisk om det finns ett litet antal dator-ID. Om användare till exempel tillåts fem datorer i sin domän, kan du söka i databasen efter de dator-ID som är kopplade till användarens användarnamn och få en liten uppsättning data för jämförelse.

Den här jämförelsen är inte praktisk för distributioner som tillåter anonym åtkomst. I det här fallet kan [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) användas. Detta ID kan dock inte vara samma om användaren öppnar innehåll från Flash och Adobe AIR®.

>[!NOTE]
>
>ID:t fungerar inte om användaren formaterar om hårddisken.

## Uppspelningsskydd {#replay-protection}

Replay-skydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan potentiellt orsaka en denial of service-attack (DoS) mot klienten.

En DoS-attack är ett försök av angripare att förhindra legitima användare av en tjänst från att använda den tjänsten. En repetitionsattack som använder rollback-räknaren kan till exempel användas för att&quot;lura&quot; licensservern att tro att DRM-klienten har återställt sitt tillstånd, vilket leder till att kontot stängs av.

Mer information om uppspelningsskydd finns i [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Underhåll en tillåtelselista med betrodda innehållspaket {#maintain-a-allowlist-of-trusted-content-packagers}

En tillåtelselista är en lista över betrodda enheter.

För innehållspaket är enheterna organisationer som av innehållsägaren är betrodda att paketera (eller kryptera) videofilerna och skapa DRM-skyddat innehåll. När du distribuerar Adobe Primetime DRM bör du ha en tillåtelselista med betrodda innehållspaket. Du måste också verifiera identiteten på innehållspaketeraren i DRM-metadata för en DRM-skyddad fil innan du kan utfärda en licens.

Mer information om hur du får information om enheten som paketerade innehållet finns i [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Timeout för autentiseringstoken{#timeout-for-authentication-tokens}

Alla autentiseringstoken som genereras av Adobe Primetime DRM SDK har ett tidsgränsintervall för att skydda programsäkerheten.

Giltigheten för autentiseringstoken anges med hjälp av DRM SDK-inställningen Primetime när en autentiseringsförfrågan hanteras. När den har gått ut är token inte längre giltig och användaren måste autentisera igen med licensservern.

Mer information om autentiseringsbegäranden finns i [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Åsidosätta principalternativ {#overriding-policy-options}

När du utfärdar en licens kan licensservern åsidosätta de användningsregler som anges i profilen.

Om principen anger ett startdatum genereras ingen licens före det startdatumet. Du kan dock ange ett framtida startdatum i licensen när licensen har skapats. Det här alternativet bör användas med försiktighet eftersom klienten inte kan hindra användaren från att flytta systemtiden framåt för att kringgå startdatumet.