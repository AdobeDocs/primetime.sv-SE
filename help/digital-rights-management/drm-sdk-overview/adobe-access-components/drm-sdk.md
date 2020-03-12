---
description: Huvudkomponenterna i Primetime DRM består av en Java SDK samt Flash Player- och Adobe AIR-klientkörningsmiljöerna.
seo-description: Huvudkomponenterna i Primetime DRM består av en Java SDK samt Flash Player- och Adobe AIR-klientkörningsmiljöerna.
seo-title: Java SDK, Flash Player och Adobe AIR-klient
title: Java SDK, Flash Player och Adobe AIR-klient
uuid: e6daed27-3803-4ef7-ba25-4a180af7502f
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM levereras som en Java SDK som innehåller de byggstenar från vilka du kan skapa en serverimplementering. Med SDK kan du skapa en Primetime DRM-lösning som passar din organisations affärsmodell.

Java-API:erna i SDK beskrivs i följande underavsnitt.

## Java-API:er för hantering av enhetsgruppsdomäner{#java-apis-for-managing-device-group-domains}

Dessa API:er används för att tillåta servern att hantera klientförfrågningar för att ansluta till och lämna enhetsgruppsdomäner.

En enhetsgruppsdomän är en logisk samling enheter som kan dela licenser mellan varandra. För att detta ska ske måste varje enhet först ansluta till/registrera sig för samma domän. Primetimes DRM SDK, som körs på en server, måste hantera förfrågningar om Device Domain-anslutning (registrering) samt begäran om Device Domain-frånkoppling (avregistrering). Enheter som inte är anslutna till någon domän kommer att få licenser som är bundna till den enheten och som inte kan delas med någon annan enhet.

## Java-API:er för att skydda innehåll{#java-apis-for-protecting-content}

Dessa API:er används för att definiera rättigheter och förbereda innehåll för distribution. API:erna för innehållsskydd är:

* Policyhantering

   API:t för principhantering används för att skapa och ändra principer som ska tillämpas på innehåll. Du kan skapa eller uppdatera profiler, inklusive hämta/ange alla användningsregler och tillåta ytterligare parametrar i ett anpassat namnutrymme.

* Innehållspaket

   Innehållspaketerings-API:t används för att kryptera innehåll och hämta metadata från det paketerade innehållet.

## Java-API:er för utfärdande av licenser{#java-apis-for-issuing-licenses}

Dessa API:er används när en klient begär en licens från servern. SDK:n stöder följande begäranden från klienten:

* Autentisering

   Autentiserings-API:t kan användas för att hantera autentiseringsbegäranden och generera autentiseringstoken.

* Generering och inköp av licenser

   API:t för licensgenerering och hämtning används för att generera en licens för användaren.

* Stöd för Adobe AIR version 1.5-klienter och Adobe AIR-innehåll

   För bakåtkompatibilitet har SDK API:er för att hantera begäranden från AIR-program som skapats för användning med AIR version 1.5 och tidigare och skyddat innehåll.

## Referensimplementering {#reference-implementation}

SDK innehåller en referensimplementering, en enkel Adobe Primetime DRM-distribution som visar hur du använder Java API:er. Referensimplementeringen innehåller en licensserver, övervakad mapppaketerare, Primetime DRM Manager AIR-program och kommandoradsverktyg för innehållspaketering och principhantering baserat på Java API:er. Mer information om implementeringen av Primetimes DRM-referens finns i Skydda innehåll.