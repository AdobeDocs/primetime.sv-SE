---
description: Om du vill fortsätta att utfärda licenser för innehåll som har paketerats med Flash Media Rights Management Server (FMRMS) 1.0 eller 1.5 måste du migrera licens- och DRM-principdata från LiveCycle ES-servern till kundens nya server som baseras på Adobe Primetime DRM SDK.
title: Migrera från FMRMS 1.0 eller 1.5 till Adobe Primetime DRM 2.0 eller senare
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Migrera från FMRMS 1.0 eller 1.5 till Adobe Primetime DRM 2.0 eller senare{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Om du vill fortsätta att utfärda licenser för innehåll som har paketerats med Flash Media Rights Management Server (FMRMS) 1.0 eller 1.5 måste du migrera licens- och DRM-principdata från LiveCycle ES-servern till kundens nya server som baseras på Adobe Primetime DRM SDK.

Utför följande uppgifter för att migrera:

1. Importlicensinformation:

   1. Information om hur du importerar licensinformation från LiveCycle ES till din Primetime DRM-baserade server finns i exempeldatabasskripten i [!DNL Reference Implementation\Server\migration\db] mapp.
   1. Kör exempelskripten för att exportera relevanta data från en MySQL-, Oracle- eller SQL Server-databas till ett CSV-filformat.
   1. Importera data till databasen när du har exporterat data från LiveCycle ES.

      Den exporterade licensinformationen innehåller följande:

      * Ett licens-ID
      * Ett innehålls-ID som tilldelas vid paketering
      * ID:t för DRM-principen som tillämpas
      * Den tid då innehållet packades
      * Innehållskrypteringsnyckeln

      Den här informationen krävs innan du kan konvertera 1.x-innehållsmetadata till Primetimes DRM-metadataformat. I referensimplementeringen lagras dessa data i databastabellen License och används av `RefImplMetadataConvReqHandler`. Mer information finns i `FMRMSv1RequestHandler` och `FMRMSv1MetadataHandler`.


1. Konvertera FMRMS-principer till Primetimes DRM-format:

   1. Innan du kan tillämpa DRM-principerna för att konvertera metadata och utfärda licenser för version 1.0- eller version 1.5-innehåll måste du konvertera befintliga DRM-principer till Primetimes DRM-format.

      The `Reference Implementation\Server\migration` -mappen innehåller exempelkod för att skapa en Primetime DRM-princip som baseras på äldre DRM-principer. Information om hur du migrerar från FMRMS 1.0 till Primetime DRM finns i `V1_0PolicyConverter.java` exempel.
   1. Kompilera exempelkoden genom att köra `ant-f build-migration.xml build-1.0-converter` skript, som söker efter DRM-biblioteken 1.0 och Primetime i [!DNL libs/1.0] och [!DNL libs/flashaccess] kataloger.

   1. Redigera [!DNL converter.properties] så att den pekar på LiveCycle ES-servern.
   1. Kör `ant -f build-migration.xml migrate-all-1.0-policies` om du vill konvertera alla DRM-principer för FMRMS 1.0 till Primetimes DRM-format.

      Information om hur du migrerar från FMRMS 1.5 till Primetime DRM finns i `V1_5PolicyConverter.java` exempel.

   1. Kompilera exempelkoden genom att köra `ant-f build-migration.xml build-1.5-converter` skript, som förväntar att 1.5- och 3.0-biblioteken ska finnas i [!DNL libs/1.5] och [!DNL libs/flashaccess] kataloger.

   1. Redigera [!DNL converter.properties] så att den pekar på LiveCycle ES-servern.
   1. Kör `ant -f build-migration.xml migrate-all-1.5-policies` om du vill konvertera alla DRM-principer för FMRMS 1.5 till Primetimes DRM-format.

      De konverterade DRM-principerna sparas som en uppsättning filer. The `DRM PolicyConverter` genererar en CSV-formaterad fil som innehåller mappning av de gamla DRM-princip-ID:n till de nya DRM-princip-ID:na. Du kan importera den här filen till [!DNL PolicyConversion] tabellen i referensimplementeringsdatabasen, där den används av `RefImplMetadataConvReqHandler`.

1. Stöd kompatibilitetsbegäranden för 1.x med `FMRMSv1RequestHandler` och `FMRMSv1MetadataHandler` egenskaper:

   1. När relevanta data har migrerats till en Primetime DRM-baserad server implementerar du stöd för 1.x-kompatibilitetsbegäranden.

      Exempel på hur du bearbetar den här typen av förfrågningar finns i `RefImplUpgradeV1ClientHandler` och `RefImplMetadataConvReqHandler` i referensimplementeringen.
