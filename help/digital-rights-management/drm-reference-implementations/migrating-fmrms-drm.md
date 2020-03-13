---
description: Om du vill fortsätta att utfärda licenser för innehåll som har paketerats med Flash Media Rights Management Server (FMRMS) 1.0 eller 1.5 måste du migrera licens- och DRM-principdata från LiveCycle ES-servern till kundens nya server som baseras på Adobe Primetime DRM SDK.
seo-description: Om du vill fortsätta att utfärda licenser för innehåll som har paketerats med Flash Media Rights Management Server (FMRMS) 1.0 eller 1.5 måste du migrera licens- och DRM-principdata från LiveCycle ES-servern till kundens nya server som baseras på Adobe Primetime DRM SDK.
seo-title: Migrera från FMRMS 1.0 eller 1.5 till Adobe Primetime DRM 2.0 eller senare
title: Migrera från FMRMS 1.0 eller 1.5 till Adobe Primetime DRM 2.0 eller senare
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Migrera från FMRMS 1.0 eller 1.5 till Adobe Primetime DRM 2.0 eller senare{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Om du vill fortsätta att utfärda licenser för innehåll som har paketerats med Flash Media Rights Management Server (FMRMS) 1.0 eller 1.5 måste du migrera licens- och DRM-principdata från LiveCycle ES-servern till kundens nya server som baseras på Adobe Primetime DRM SDK.

Utför följande uppgifter för att migrera:

1. Importlicensinformation:

   1. Information om hur du importerar licensinformation från LiveCycle ES till din Primetime DRM-baserade server finns i exempeldatabasskripten i [!DNL Reference Implementation\Server\migration\db] mappen.
   1. Kör exempelskripten för att exportera relevanta data från en MySQL-, Oracle- eller SQL Server-databas till ett CSV-filformat.
   1. Importera data till databasen när du har exporterat dem från LiveCycle ES.

      Den exporterade licensinformationen innehåller följande:

      * Ett licens-ID
      * Ett innehålls-ID som tilldelas vid paketering
      * ID:t för DRM-principen som tillämpas
      * Den tid då innehållet packades
      * Innehållskrypteringsnyckeln
      Den här informationen krävs innan du kan konvertera 1.x-innehållsmetadata till Primetimes DRM-metadataformat. I referensimplementeringen lagras dessa data i licenstabellen och används av `RefImplMetadataConvReqHandler`. For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.


1. Konvertera FMRMS-principer till Primetimes DRM-format:

   1. Innan du kan tillämpa DRM-principerna för att konvertera metadata och utfärda licenser för version 1.0- eller version 1.5-innehåll måste du konvertera befintliga DRM-principer till Primetimes DRM-format.

      Mappen innehåller exempelkod för att skapa en Primetime DRM-princip som baseras på äldre DRM-principer. `Reference Implementation\Server\migration` Information om hur du migrerar från FMRMS 1.0 till Primetime DRM finns i exemplet `V1_0PolicyConverter.java` .
   1. Kompilera exempelkoden genom att köra `ant-f build-migration.xml build-1.0-converter` skript som söker efter DRM-biblioteken 1.0 och Primetime i [!DNL libs/1.0] - och [!DNL libs/flashaccess] -katalogerna.

   1. Redigera [!DNL converter.properties] filen så att den pekar på LiveCycle ES-servern.
   1. Kör `ant -f build-migration.xml migrate-all-1.0-policies` för att konvertera alla DRM-principer för FMRMS 1.0 till Primetimes DRM-format.

      Information om hur du migrerar från FMRMS 1.5 till Primetime DRM finns i exemplet `V1_5PolicyConverter.java` .

   1. Kompilera exempelkoden genom att köra `ant-f build-migration.xml build-1.5-converter` skript som förväntar att biblioteken 1.5 och 3.0 ska finnas i [!DNL libs/1.5] - och [!DNL libs/flashaccess] -katalogerna.

   1. Redigera [!DNL converter.properties] filen så att den pekar på LiveCycle ES-servern.
   1. Kör `ant -f build-migration.xml migrate-all-1.5-policies` för att konvertera alla DRM-principer för FMRMS 1.5 till Primetimes DRM-format.

      De konverterade DRM-principerna sparas som en uppsättning filer. Den `DRM PolicyConverter` genererar en CSV-formaterad fil som inkluderar mappning av de gamla DRM-princip-ID:n till de nya DRM-princip-ID:na. Du kan importera den här filen till [!DNL PolicyConversion] tabellen i referensimplementeringsdatabasen, där den används av `RefImplMetadataConvReqHandler`.

1. Stöd för 1.x-kompatibilitetsbegäranden med `FMRMSv1RequestHandler` och `FMRMSv1MetadataHandler` egenskaper:

   1. När relevanta data har migrerats till en Primetime DRM-baserad server implementerar du stöd för 1.x-kompatibilitetsbegäranden.

      Exempel på hur du bearbetar den här typen av begäranden finns i `RefImplUpgradeV1ClientHandler` och `RefImplMetadataConvReqHandler` i referensimplementeringen.

