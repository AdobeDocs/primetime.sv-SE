---
seo-title: BEES-felkoder
title: BEES-felkoder
uuid: 7b2d0dd1-9a43-47e3-b932-a4eaf784ae7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# BEES-felkoder {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Om ett fel uppstår under en BEES-kontroll `DRMErrorEvent` returneras klienten. Du kan analysera den här händelsens egenskaper för att hitta information om felets karaktär. En deluppsättning med möjliga felkoder visas nedan.

| Fel | Beskrivning |
|---|---|
| `3304:305` | Allmänt auktoriseringsfel från Primetime Cloud DRM som försöker hantera en autentiserings-/auktoriseringsbegäran. Vanligtvis inte kopplat till ett BEES-problem. Om felet kvarstår bör du skicka en felanmälan till Primetimes DRM-team tillsammans med diagnostikinformation. |
| `3329:0` | Programspecifikt fel (från BEES Authorizer). Om ingen underfelkod returnerades visas feltexten. Det uppstod till exempel ett problem med att analysera svaret eller så gick det inte att nå BEES-servern. |
| `3329:<HTTP error code>` | Ett annat HTTP-svar än 200 utfärdades av BEES-servern. HTTP-felkoden returneras till klienten i kodfältet för underfel. Detta kan tyda på ett konfigurationsproblem eller ett fel på BEES-servern. |
| `3329:<x>` | BEES-servern INAKTIVERADE licensbegäran. Underfelkoden och feltexten anges av BEES-servern i JSON-svarets `error` - och `errorText` -egenskaper. Den här typen av svar bör inte betraktas som ett fel, utan snarare som ett vanligt denial-svar från BEES-servern. |