---
seo-title: Distribuera Adobe Primetime DRM
title: Distribuera Adobe Primetime DRM
uuid: c14c2792-d207-4f39-b856-610520bdaa28
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Distribuera Adobe Primetime DRM {#configure-adobe-primetime-drm}

En viktig fördel med Adobe Primetime DRM SDK är att du kan installera den på en Java™-programserver eller serverbehållare som Tomcat. Du behöver också JDK™ 1.5 eller senare. Mer information om programvarukrav finns i Plattformskrav för Primetime DRM SDK: [https://www.adobe.com/products/flashaccess/systemreqs/](https://www.adobe.com/products/flashaccess/systemreqs/).

Steg på hög nivå för att distribuera Primetime DRM är:

1. Installera och konfigurera Primetime DRM SDK.
1. Hämta digitala certifikat från Adobe.
1. Skapa en licensserver med SDK eller distribuera Primetime DRM-servern för skyddad direktuppspelning.
1. Skapa innehållspaket och principhanteringsverktyg för att paketera innehåll, använda de medföljande verktygen för innehållsförberedelse eller licensiera en av paketen i Adobe HTTP Dynamic Streaming.
1. Definiera användningsregler för ditt innehåll och skapa profiler som stöder dessa regler.
1. Paketera innehållet med hjälp av paketerings- och policyhanteringsverktygen.
1. Utveckla videoapplikationer som kunderna kan använda för att visa skyddat innehåll med Flash Player eller Adobe AIR, eller använd en etablerad OVP (Online Video Platform) som stöder Primetime DRM.
1. Distribuera en SWF-fil för användning med Flash Player på webbplatsen eller lägg upp installationsprogrammet för Adobe AIR för nedladdning.

De här stegen beskrivs närmare i följande avsnitt, med referenser till andra dokument som innehåller ytterligare information.

## Distribuera på ett 64-bitars operativsystem{#deploying-on-a-bit-operating-system}

Ett 64-bitars operativsystem, som 64-bitarsversionen av RedHat eller Windows, ger mycket bättre prestanda än ett 32-bitars operativsystem.

## Installera Adobe Primetime DRM SDK {#install-adobe-primetime-drm-sdk}

Primetime DRM SDK tillhandahålls som en Java-arkivfil (JAR). Mer information om hur du installerar Primetime DRM finns i Använda Adobe Primetime DRM SDK för att skydda innehåll och riktlinjerna för säker distribution.

## Implementera en licensserver {#implement-a-license-server}

Med Adobe Primetime DRM SDK måste du skapa en licensserver. När innehåll skyddas med Primetime DRM kan det inte visas förrän en licens har utfärdats till konsumenten av licensservern. Om identitetsbaserad licensiering används säkerställer lösenordsbaserad autentisering att bara behöriga konsumenter kan öppna och visa innehållet.

När du implementerar en licensserver måste du skaffa de nödvändiga digitala certifikaten från Adobe. Mer information om hur du begär certifikat finns i dokumentet om registrering av DRM-certifikat i Primetime.

Mer information om hur du implementerar en licensserver och hämtar digitala certifikat finns i **Använda Adobe Primetime DRM SDK för att skydda innehåll.**

## Skapa innehållspaket och principhanteringsverktyg{#create-content-packaging-and-policy-management-tools}

Med Adobe Primetime DRM SDK kan du skapa innehållspaket och principhanteringsverktyg. Med API:erna för principhantering kan administratörer skapa, visa information om och uppdatera principer. Paketerings-API:erna bäddar in principen i videofilen och krypterar filen med hjälp av innehållskrypteringsnyckeln.

Primetimes DRM SDK innehåller en referensimplementering ( [!DNL AdobePackager.jar]) som innehåller exempel på innehållspaket och principhanteringsverktyg ( [!DNL AdobePolicyManager.jar]).

Mer information om hur du skapar innehållspaket och principhanteringsverktyg finns i **Använda Adobe Primetime DRM SDK för att skydda innehåll.**

## Skapa profiler och paketera innehåll {#create-policies-and-package-content}

Med de användningsregler som stöds av SDK måste ni definiera och skapa profiler som stöder er organisations affärsmodell och sedan paketera innehållet med dessa profiler. När reglerna tillämpas på innehållet under paketeringen kan ni behålla kontrollen över innehållet oavsett hur brett det distribueras.

Profilerna i Adobe Primetime DRM har stöd för en mängd olika användningsregler, bland annat:

* Ange hur många dagar en licens är giltig när en konsument börjar titta på innehållet.
* Tillåter licenscache-lagring.
* Ange klientkörningsmiljöer och versioner som kan komma åt innehåll (användare måste till exempel ha ett visst Adobe AIR-program eller en viss version av Flash Player).
* Kräver att konsumenterna autentiserar sig med ett användarnamn och lösenord innan de kan visa skyddat innehåll eller tillåta anonym åtkomst.

Mer information om att paketera innehåll finns i *Skydda innehåll*. Mer information om användningsregler och vilka affärsmodeller de stöder finns i *Användningsregler*.

## Utveckla program för videouppspelning {#develop-applications-for-video-playback}

Om du vill att tittarna ska kunna få tillgång till och visa innehåll utvecklar du ett videouppspelningsprogram med Flash Player eller Adobe AIR. När du väl har utvecklat ett videouppspelningsprogram måste du distribuera det till konsumenterna. Om du utvecklar ett program med Flash Player ska du lägga det på din organisations webbplats. Om du utvecklar ett program med Adobe® AIR® skickar du AIR-programmets installationsprogram så att användarna kan hämta och installera programmet på sina datorer.

Mer information om hur du utvecklar anpassade videouppspelningsprogram för användning med Adobe Primetime DRM finns i kapitlet&quot;Arbeta med video&quot; i [Utvecklarhandbok för ActionScript 3.0](https://help.adobe.com/en_US/as3/dev/WS9936fa0d5984e93b3f4f38ec1272a447844-8000.html), [Adobe Video Technology Center](https://www.adobe.com/devnet/video/) samt i Open Source Media Framework.