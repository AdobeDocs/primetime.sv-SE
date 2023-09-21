---
title: BEES-felkoder
description: BEES-felkoder
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# BEES-felkoder {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Om det uppstår ett fel under en BEES-kontroll kan du `DRMErrorEvent` returneras till klienten. Du kan analysera den här händelsens egenskaper för att hitta information om felets karaktär. En deluppsättning med möjliga felkoder visas nedan.

| Fel | Beskrivning |
|---|---|
| `3304:305` | Allmänt auktoriseringsfel från Primetime Cloud DRM som försöker hantera en autentiserings-/auktoriseringsbegäran. Vanligtvis inte kopplat till ett BEES-problem. Om felet kvarstår bör du skicka en felanmälan till Primetimes DRM-team tillsammans med diagnostikinformation. |
| `3329:0` | Programspecifikt fel (från BEES Authorizer). Om ingen underfelkod returnerades visas feltexten. Det uppstod till exempel ett problem när svaret skulle tolkas, eller så gick det inte att nå BEES-servern. |
| `3329:<HTTP error code>` | Ett annat HTTP-svar än 200 utfärdades av BEES-servern. HTTP-felkoden returneras till klienten i kodfältet för underfel. Detta kan tyda på ett konfigurationsproblem eller ett fel på BEES-servern. |
| `3329:<x>` | BEES-servern INAKTIVERADE licensbegäran. Underfelkoden och feltexten anges av BEES-servern i JSON-svarets `error` och `errorText` egenskaper. Den här typen av svar bör inte betraktas som ett fel, utan snarare som ett vanligt denial-svar från BEES-servern. |
