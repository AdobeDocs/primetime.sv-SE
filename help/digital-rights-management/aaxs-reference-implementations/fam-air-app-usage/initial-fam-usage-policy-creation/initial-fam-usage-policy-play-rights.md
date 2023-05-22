---
title: Uppspelningsrättigheter
description: Uppspelningsrättigheter
copied-description: true
exl-id: a4fda537-dbcc-496b-8f15-c13b25fe87b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Uppspelningsrättigheter {#play-rights}

I följande tabell beskrivs inställningarna för uppspelningsrättigheter:

| Inställningar | Beskrivning |
|--- |--- |
| Uppspelningsfönster | Den tid en licens är giltig (i minuter) efter första gången användaren spelar upp det skyddade innehållet. |
| Utdataskydd | Anger om utdata till externa återgivningsenheter ska skyddas. Analoga och digitala utdata kan anges oberoende av varandra. |
| Begränsningar | Blockeringslista i klientversioner tillåts inte att spela upp innehåll. Alla kolumner är valfria. |
| DRM | Anger en lista över DRM-versioner som inte får spela upp skyddat innehåll. |
| Körning | Anger en lista med körningsmiljöversioner som inte får spela upp skyddat innehåll. |
| Minsta säkerhetsnivå |  |
| DRM | Den lägsta DRM-säkerhetsnivå som krävs för att spela upp skyddat innehåll. |
| Körning | Den lägsta säkerhetsnivå vid körning som krävs för att spela upp skyddat innehåll. |
| Tillåtna program | Tillåtelselista av klientprogram som får spela upp innehåll. Om inga program anges tillåts alla program i SWF eller AIR. |
| SWF | Lista över SWF-URL:er som får spela upp skyddat innehåll. |
| AIR | Lista över AIR-program som får spela upp skyddat innehåll. Utgivar-ID krävs, de återstående fälten är valfria. |

Flash Access Manager stöder principer som innehåller flera uppspelningsrättigheter. Om du vill skapa en profil med mer än en uppspelningsrättighet använder du knappen &quot;Lägg till ytterligare uppspelningsrättighet&quot; och fyller i önskade attribut för varje uppspelningsrättighet.

När kunden förbrukar en licens används den första uppspelningsrättigheten som den uppfyller alla krav för. Flera uppspelningsrättigheter kan användas för att ange olika begränsningar för olika operativsystem. Det är till exempel möjligt att ange en rättighet med utdataskydd som krävs för Windows (genom att blockera DRM-versioner på Macintosh och Linux) och att ange en andra rättighet med utdataskydd som&quot;Använd om tillgängligt&quot; på andra plattformar (genom att blockera DRM-versioner på Windows).
