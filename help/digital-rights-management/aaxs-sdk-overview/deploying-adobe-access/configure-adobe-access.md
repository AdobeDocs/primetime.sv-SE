---
seo-title: Distribuera Adobe Access
title: Distribuera Adobe Access
uuid: 9f9a9931-f607-4b1a-9209-0236a4c197ca
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Distribuera Adobe Access {#deploy-adobe-access}

En viktig fördel med Adobe Access SDK är att du kan installera den på alla Java™-programservrar och serverbehållare, som Tomcat. Du behöver också JDK™ 1.5 eller senare. Mer information om programvarukrav finns i plattformskraven för Adobe Access SDK: [: https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Följande åtgärder på hög nivå krävs för att distribuera Adobe Access:

1. Installera och konfigurera Adobe Access SDK.
1. Hämta digitala certifikat från Adobe.
1. Skapa en licensserver med SDK eller distribuera Adobe Access Server för skyddad strömning.
1. Skapa innehållspaket och principhanteringsverktyg för att paketera innehåll, använda de medföljande verktygen för innehållsförberedelse eller licensiera en av paketen i Adobe HTTP Dynamic Streaming.
1. Definiera användningsregler för ditt innehåll och skapa profiler som stöder dessa regler.
1. Paketera innehållet med hjälp av paketerings- och policyhanteringsverktygen.
1. Utveckla videoapplikationer som kunderna kan använda för att visa skyddat innehåll med hjälp av Flash Player eller Adobe AIR, eller använda en väletablerad OVP (Online Video Platform) som stöder Adobe Access.
1. Distribuera en SWF-fil för användning med Flash Player på webbplatsen eller lägg upp installationsprogrammet för Adobe AIR för nedladdning.

De här stegen beskrivs närmare i följande avsnitt, med referenser till andra dokument som innehåller ytterligare information.

## Distribuera på ett 64-bitars operativsystem {#deploying-on-a-bit-operating-system}

Ett 64-bitars operativsystem, som 64-bitarsversionen av RedHat eller Windows, ger mycket bättre prestanda än ett 32-bitars operativsystem.

## Installera Adobe Access SDK {#install-adobe-access-sdk}

Adobe Access SDK tillhandahålls som en Java-arkivfil (JAR). Mer information om hur du installerar Adobe Access finns i *Använda Adobe Access SDK för att skydda innehåll* och *Riktlinjer för säker distribution*.

## Implementera en licensserver {#implement-a-license-server}

Med Adobe Access SDK måste du skapa en licensserver. När innehåll skyddas med Adobe Access kan det inte visas förrän en licens har utfärdats till konsumenten av licensservern. Om identitetsbaserad licensiering används säkerställer lösenordsbaserad autentisering att bara behöriga konsumenter kan öppna och visa innehållet.

När du implementerar en licensserver måste du skaffa de nödvändiga digitala certifikaten från Adobe. Mer information om hur du begär certifikat finns i dokumentet om registrering av åtkomstcertifikat i Adobe.

Mer information om hur du implementerar en licensserver och skaffar digitala certifikat finns i* Använda Adobe Access SDK för att skydda innehåll.*

## Skapa innehållspaket och principhanteringsverktyg {#create-content-packaging-and-policy-management-tools}

Med Adobe Access SDK kan du skapa innehållspaket och principhanteringsverktyg. Med API:erna för principhantering kan administratörer skapa, visa information om och uppdatera principer. Paketerings-API:erna bäddar in profilen i FLV- eller F4V-filen och krypterar filen med krypteringsnyckeln för innehållet.

Adobe Access SDK innehåller en referensimplementering ( [!DNL AdobePackager.jar]) som innehåller exempel på innehållspaket och principhanteringsverktyg ( [!DNL AdobePolicyManager.jar]).

Mer information om hur du skapar innehållspaket och principhanteringsverktyg finns i *Använda Adobe Access SDK för att skydda innehåll*.

## Skapa profiler och paketera innehåll {#create-policies-and-package-content}

Med de användningsregler som stöds av SDK måste ni definiera och skapa profiler som stöder er organisations affärsmodell och sedan paketera innehållet med dessa profiler. När reglerna tillämpas på innehållet under paketeringen kan ni behålla kontrollen över innehållet oavsett hur brett det distribueras.

Policyerna i Adobe Access stöder ett stort antal olika användningsregler, bland annat:

* Ange hur många dagar en licens är giltig när en konsument börjar titta på innehållet.
* Tillåter licenscache-lagring.
* Ange klientkörningsmiljöer och versioner som kan komma åt innehåll (användare måste till exempel ha ett visst Adobe AIR-program eller en viss version av Flash Player).
* Kräver att konsumenterna autentiserar sig med ett användarnamn och lösenord innan de kan visa skyddat innehåll eller tillåta anonym åtkomst.

Mer information om att paketera innehåll finns i *Skydda innehåll*. Mer information om användningsregler och vilka affärsmodeller de stöder finns i *Användningsregler*.

## Utveckla program för videouppspelning {#develop-applications-for-video-playback}

Om du vill att tittarna ska kunna få tillgång till och visa innehåll utvecklar du ett videouppspelningsprogram med Flash Player eller Adobe AIR. När du väl har utvecklat ett videouppspelningsprogram måste du distribuera det till konsumenterna. Om du utvecklar ett program med Flash Player ska du lägga det på din organisations webbplats. Om du utvecklar ett program med Adobe® AIR® skickar du AIR-programmets installationsprogram så att användarna kan hämta och installera programmet på sina datorer.

Mer information om hur du utvecklar anpassade videouppspelningsprogram som ska användas med Adobe Access finns i kapitlet&quot;Arbeta med video&quot; i [Utvecklarhandbok för ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html)*, *i [Adobe Video Technology Center](https://www.adobe.com/devnet/video/) och i Open Source Media Framework.