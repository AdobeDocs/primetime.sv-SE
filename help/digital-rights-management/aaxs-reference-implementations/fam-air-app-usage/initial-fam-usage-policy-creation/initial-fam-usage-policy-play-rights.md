---
seo-title: Uppspelningsrättigheter
title: Uppspelningsrättigheter
uuid: 90f2a7a6-6637-4d10-9afe-6d2e77fc4185
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
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
| Begränsningar | Blocklista över klientversioner som inte får spela upp innehåll. Alla kolumner är valfria. |
| DRM | Anger en lista över DRM-versioner som inte får spela upp skyddat innehåll. |
| Körning | Anger en lista med körningsmiljöversioner som inte får spela upp skyddat innehåll. |
| Minsta säkerhetsnivå |  |
| DRM | Den lägsta DRM-säkerhetsnivå som krävs för att spela upp skyddat innehåll. |
| Körning | Den lägsta säkerhetsnivå vid körning som krävs för att spela upp skyddat innehåll. |
| Tillåtna program | Tillåt en lista över klientprogram som får spela upp innehåll. Om inga program anges tillåts alla SWF- och AIR-program. |
| SWF | Lista över SWF-URL:er som får spela upp skyddat innehåll. |
| AIR | Lista över AIR-program som tillåts spela upp skyddat innehåll. Utgivar-ID krävs, de återstående fälten är valfria. |

Flash Access Manager stöder principer som innehåller flera uppspelningsrättigheter. Om du vill skapa en profil med mer än en uppspelningsrättighet använder du knappen &quot;Lägg till ytterligare uppspelningsrättighet&quot; och fyller i de önskade attributen för varje uppspelningsrättighet.

När kunden förbrukar en licens används den första uppspelningsrättigheten som den uppfyller alla krav för. Flera uppspelningsrättigheter kan användas för att ange olika begränsningar för olika operativsystem. Det är till exempel möjligt att ange en rättighet med utdataskydd som krävs för Windows (genom att blockera DRM-versioner på Macintosh och Linux) och att ange en andra rättighet med utdataskydd som&quot;Använd om tillgängligt&quot; på andra plattformar (genom att blockera DRM-versioner på Windows).
