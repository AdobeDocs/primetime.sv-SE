---
title: Migrera från FMRMS 1.0 eller 1.5 till Adobe Access 2.0 och senare
description: Migrera från FMRMS 1.0 eller 1.5 till Adobe Access 2.0 och senare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Migrera från FMRMS 1.0 eller 1.5 till Adobe Access 2.0 och senare {#migrating-from-fmrms-or-to-adobe-access-and-above}

För att kunna fortsätta att utfärda licenser för innehåll som paketerats med Flash Media Rights Management Server (FMRMS) 1.0 eller 1.5 måste licens- och policydata migreras från LiveCycle ES-servern till kundens nya server baserat på Adobe Access SDK. De viktiga stegen är:

1. Importera licensinformation
1. Konvertera FMRMS-principer till Adobe Access-format
1. Stöd för 1.x-kompatibilitetsbegäranden via `FMRMSv1RequestHandler` och `FMRMSv1MetadataHandler`

Om du vill importera licensinformation från LiveCycle ES till den Adobe Access-baserade servern läser du exempeldatabasskripten i [!DNL Reference Implementation\Server\migration\db] mapp. Exempelskript finns för export av relevanta data från en MySQL-, Oracle- eller SQL Server-databas till ett CSV-filformat. När du har exporterat data kan du importera dem till valfri databas. Den exporterade licensinformationen innehåller licens-ID, ett innehålls-ID som tilldelats vid paketeringen, ID:t för profilen som användes, tidpunkten då innehållet packades samt krypteringsnyckeln för innehållet. För Adobe Access krävs den här informationen för att konvertera 1.x-innehållets metadata till metadataformatet för Adobe Access (se `FMRMSv1RequestHandler` och `FMRMSv1MetadataHandler`). I referensimplementeringen lagras dessa data i licenstabellen och används av `RefImplMetadataConvReqHandler`.

Befintliga policyer måste konverteras till Adobe Access-format för att kunna använda dessa policyer vid konvertering av metadata och utfärdande av licenser för 1.0- eller 1.5-innehåll. Mappen Reference Implementation\Server\Migration innehåller exempelkod för att skapa en Adobe Access-princip baserad på äldre principer.

Om du migrerar från FMRMS 1.0 till Adobe Access läser du exemplet V1_0PolicyConverter.java. Kompilera exempelkoden genom att köra &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (skriptet förväntar att biblioteken 1.0 och Adobe Access ska vara i [!DNL libs/1.0] och libs/flashaccess). Redigera filen converter.properties så att den pekar på LiveCyclets ES-server. Kör sedan &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; om du vill konvertera alla FMRMS 1.0-principer till Adobe Access-format.

Om du migrerar från FMRMS 1.5 till Adobe Access läser du exemplet V1_5PolicyConverter.java. Kompilera exempelkoden genom att köra &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (skriptet förväntar att 1.5- och 3.0-biblioteken ska finnas i libs/1.5 respektive libs/flashaccess). Redigera filen converter.properties så att den pekar på LiveCyclets ES-server. Kör sedan &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; om du vill konvertera alla FMRMS 1.5-principer till Adobe Access-format.

De konverterade profilerna skrivs till en uppsättning filer. Dessutom kommer PolicyConverter att generera en CSV-fil som innehåller mappning av gamla princip-ID:n till nya princip-ID:n. Den här filen kan importeras till registret PolicyConversion i referensimplementeringsdatabasen och kommer att användas av `RefImplMetadataConvReqHandler`.

När relevanta data har migrerats till din Adobe Access-baserade server kan du implementera stöd för 1.x-kompatibilitetsbegäranden. Se `RefImplUpgradeV1ClientHandler` och `RefImplMetadataConvReqHandler` i referensimplementeringen för exempel på hur dessa typer av begäranden ska behandlas.
