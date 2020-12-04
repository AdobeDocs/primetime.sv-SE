---
description: Huvudkomponenterna i Adobe Access består av en Java SDK och klientmiljöerna för Flash Player och Adobe AIR.
seo-description: Huvudkomponenterna i Adobe Access består av en Java SDK och klientmiljöerna för Flash Player och Adobe AIR.
seo-title: Java SDK, Flash Player och Adobe AIR-klient
title: Java SDK, Flash Player och Adobe AIR-klient
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Adobe Access-komponenter{#adobe-access-components}

Huvudkomponenterna i Adobe Access består av en Java SDK och klientmiljöerna för Flash Player och Adobe AIR.

Mer information om hur du konfigurerar SDK finns i Konfigurera SDK i *Använda Adobe Access SDK för att skydda innehåll.*

Med Adobe Access SDK kan ni utveckla en digital rättighetshanteringslösning som är integrerad med organisationens befintliga affärsinfrastruktur, till exempel system för innehållshantering, fakturering och användaråtkomstkontroll. Med Flash Player och Adobe AIR kan ni skapa och enkelt driftsätta applikationer som kunderna kan använda för att öppna och visa stora bibliotek med digitalt innehåll.

## Adobe Access SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access levereras som en Java SDK som innehåller de byggstenar som du kan använda för att skapa en serverimplementering. Med SDK kan du skapa en Adobe Access-lösning som passar din organisations affärsmodell.

Java-API:erna i SDK beskrivs i följande underavsnitt.

## Java-API:er för hantering av enhetsgruppsdomäner {#java-apis-for-managing-device-group-domains}

Dessa API:er används för att tillåta servern att hantera klientförfrågningar för att ansluta till och lämna enhetsgruppsdomäner.

En enhetsgruppsdomän är en logisk samling enheter som kan dela licenser mellan varandra. För att detta ska ske måste varje enhet först ansluta till/registrera sig för samma domän. Adobe Access SDK, som körs på en server, måste hantera förfrågningar om Device Domain-anslutning (registrering) samt begäran om Device Domain-frånkoppling (avregistrering). Enheter som inte är anslutna till någon domän kommer att få licenser som är bundna till den enheten och som inte kan delas med någon annan enhet.

## Java-API:er för att skydda innehåll {#java-apis-for-protecting-content}

Dessa API:er används för att definiera rättigheter och förbereda innehåll för distribution. API:erna för innehållsskydd är:

* Policyhantering

   API:t för principhantering används för att skapa och ändra principer som ska tillämpas på innehåll. Du kan skapa eller uppdatera profiler, inklusive hämta/ange alla användningsregler och tillåta ytterligare parametrar i ett anpassat namnutrymme.

* Innehållspaket

   Innehållspaketerings-API:t används för att kryptera innehåll och hämta metadata från det paketerade innehållet.

## Java API:er för utfärdande av licenser {#java-apis-for-issuing-licenses}

Dessa API:er används när en klient begär en licens från servern. SDK:n stöder följande begäranden från klienten:

* Autentisering

   Autentiserings-API:t kan användas för att hantera autentiseringsbegäranden och generera autentiseringstoken.

* Generering och inköp av licenser

   API:t för licensgenerering och hämtning används för att generera en licens för användaren.

* Stöd för Adobe AIR version 1.5-klienter och innehåll

   För bakåtkompatibilitet har SDK API:er för att hantera begäranden från AIR-program som skapats för användning med AIR version 1.5 och tidigare och skyddat innehåll.

## Referensimplementering {#reference-implementation}

SDK innehåller en referensimplementering, en enkel Adobe Access-distribution som visar hur du använder Java API:er. Referensimplementeringen innehåller en licensserver, övervakad mapppaketerare, Adobe Access Manager AIR-program och kommandoradsverktyg för innehållspaketering och principhantering baserat på Java API:erna. Mer information om referensimplementeringen av Adobe Access finns i *Skydda innehåll*.

## Adobe Access Server for Protected Streaming {#adobe-access-server-for-protected-streaming}

För direktuppspelning där innehåll skyddas med Adobe Access, t.ex. Adobe HTTP Dynamic Streaming, ingår även Adobe Access Server för skyddad direktuppspelning. Lösningen kan enkelt driftsättas i en serverbehållare som Tomcat och kan uppnå en hög nivå av skalbarhet och prestanda för att uppfylla de största behoven för innehållsdistribution.

## Adobe Flash Player {#adobe-flash-player}

Flash Player är en lättviktig webbläsarplugin och runtime som ger enhetliga och engagerande användarupplevelser, enastående ljud-/videouppspelning och stor räckvidd. Flash Player ger högkvalitativ uppspelning av direktuppspelat eller nedladdat videoinnehåll. För utgivare av innehåll kan Flash Player anpassa uppspelningsskärmarna runt innehållet, vilket ger större varumärkesupplevelser och intäktsgenerering genom annonser med banners och överlägg. För kunderna är Flash Player ett intuitivt och visuellt tilltalande sätt att visa videoinnehåll.

Mer information om Flash Player finns på [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR är en operativsystemsoberoende runtime som gör det möjligt för innehållsproducenter att utöka sina befintliga webbinvesteringar till datorn genom att designa anpassade multimedieprogram. Den bygger på beprövade, öppna teknologier och är ett tillförlitligt och förenklat sätt för företag att utveckla och driftsätta skräddarsydda applikationer som är tillförlitliga och ger en säkrare och roligare användarupplevelse. Med Adobe AIR kan företag enkelt integrera multimedia för att skapa en mer engagerande och interaktiv användarupplevelse. Det gör att utvecklare kan använda välkända verktyg som HTML, JavaScript, Flash och Adobe® Flex® för att driftsätta en unik kombination av RIA-program i Windows, Macintosh och Linux.

Företag har fullständig kontroll över användargränssnittet och kan utforma en användarupplevelse som speglar och stärker deras varumärke. Med inbyggt stöd för uppspelning av innehåll som skyddas med Adobe Access SDK kan Adobe AIR skapa anpassade och kompletta innehållsdistributionskedjor.

Mer information om Adobe AIR finns här: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Inbyggda iOS- och Android-program {#native-ios-and-android-applications}

Inbyggda iOS- och Android-program som endast är tillgängliga för Adobe Primetime-kunder kan användas med Adobe Access DRM 4.0 eller senare för att skydda video som används i inbyggda (ej Flash) program på mobila enheter. För att ett program ska kunna använda det här skyddade innehållet måste det implementeras med Adobe Primetime Client Libraries.

Mer information om Adobe Primetime finns här: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)