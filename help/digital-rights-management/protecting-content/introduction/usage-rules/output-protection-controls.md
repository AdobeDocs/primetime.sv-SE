---
seo-title: Skydd av utdata
title: Skydd av utdata
uuid: a0518392-cd33-4ef0-834c-f90145a9b421
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Skydd av utdata{#output-protection-controls}

Utdataskyddet styr parametern om utdata till externa återgivningsenheter är skyddade. Du kan ange begränsningar för analoga och digitala utdata oberoende av varandra.

Anger om utdata till externa återgivningsenheter ska begränsas. En extern enhet definieras som en video- eller ljudenhet som inte är inbäddad i datorn. Integrerade bildskärmar, t.ex. bärbara datorer, anses inte vara externa i scenariot för utdataskydd.

OTA-anslutningstyperna (air) listas som standard, men kan anges explicit om det behövs. Följande OTA-anslutningar stöds: Miracast, AirPlay, DLNA och WIDI.

**Upplösningsbaserat utdataskydd: (Tillgängligt från version 5.3 och framåt.) ** Detta ger utdataskydd baserat på det lodräta pixelantalet i innehållet, vilket gör det möjligt att ange en mängd skyddskrav baserat på antalet lodräta pixlar.

Följande alternativ/efterlevnadsnivåer är tillgängliga:

| Alternativ | Stöds i analoga enheter | Stöds i digitala enheter |
|---|---|---|
| **Obligatoriskt** - AVS-utdataskydd (Analog Copy Protection) eller CGMS-A-utdataskydd (Copy Generation Management System) måste aktiveras för att innehållet ska kunna spelas upp på en extern enhet. Primetime DRM-klienter måste aktivera utdataskydd med hjälp av ACP eller CGMS-A. På enheter som stöder båda försöker Primetime DRM 3.0-klienterna aktivera båda. Endast en måste dock vara aktiverad för att innehållet ska kunna spelas upp. | JA | JA |
| **Krävs** för AVS-stater - AVS-stater måste ha skydd för utdata. Uppspelning tillåts inte på CGMS-A. Primetime DRM 2.0-klienter stöder inte det här alternativet. Om detta anges fungerar en Primetime DRM 2.0-klient som om alternativet Ingen uppspelning har angetts. | JA | - |
| **Använd om tillgängligt** - Försök att aktivera AVS- och CGMS-A-utdataskydd om det är tillgängligt och tillåt uppspelning om det inte är tillgängligt. Primetime DRM 3.0-klienter försöker aktivera både ACP och CGMS-A, om möjligt. Primetime DRM 2.0-klienter försöker bara aktivera antingen ACP eller CGMS-A. Ett försök görs av Primetime DRM-klienten att aktivera antingen ACP eller CGMS-A. Om försöket lyckas kan det andra alternativet inte aktiveras. Om försöket misslyckas görs sedan ett andra försök att aktivera det andra alternativet. Även om båda försöken misslyckas spelas innehållet upp ändå. | JA | JA |
| **Använd ACP om det finns** - försök att aktivera AVS-utdataskydd om tillgängligt, men tillåt uppspelning om det inte finns tillgängligt. Skydd är inte tillgängligt på CGMS-A. Primetime DRM 2.0-klienter stöder inte det här alternativet. Om detta anges fungerar en Primetime DRM 2.0-klient som om alternativet Inget skydd har angetts. | JA | - |
| **Använd CGMS-A om tillgängligt **— Försök aktivera CGMS-A-utdataskydd om det är tillgängligt, men tillåt uppspelning om det inte är tillgängligt. Skydd är inte tillgängligt på AVS. Primetime DRM 2.0-klienter stöder inte det här alternativet. Om detta anges fungerar en Primetime DRM 2.0-klient som om alternativet Inget skydd har angetts. | JA | - |
| **Inget skydd** - Ingen aktivering av utdataskydd krävs för analoga och digitala utdata. | JA | JA |
| **Ingen uppspelning** - Tillåt inte uppspelning till en extern enhet för analoga och digitala utdata. | JA | JA |

>[!NOTE]
>
>Dessa regler används konsekvent på alla plattformar, men du kan bara på ett säkert sätt aktivera utdataskydd på Windows-plattformar. På andra plattformar, till exempel Macintosh och Linux, finns det inga operativsystemsfunktioner som stöds tillgängliga för tredjepartsprogram.

Exempel: En del innehåll kan framtvinga utdataskyddskontroller och därför kan innehållsdistributören ange skyddsnivån. Om&quot;Obligatoriskt&quot; har angetts och uppspelningsförsök görs på en Macintosh spelas inte innehållet upp på externa enheter. Innehållet kan spelas upp på interna bildskärmar.

Om&quot;Obligatoriskt&quot; anges och uppspelningsförsök görs på Linux, spelas inte innehållet upp på någon enhet eftersom det inte går att skilja mellan interna och externa enheter.

Om du anger &quot;Använd om tillgängligt&quot; aktiveras utdataskyddet där det är möjligt. På Windows-system som stöder Certified Output Protection Protocol (COPP) skickas innehållet med utdataskydd till en extern skärm. Det här exemplet kallas ibland *`selectable output control`*.
