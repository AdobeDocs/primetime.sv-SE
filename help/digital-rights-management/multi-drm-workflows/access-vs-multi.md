---
description: För dem som är bekanta med Adobe Primetime Access DRM-lösningen finns det vissa grundläggande arkitektoniska skillnader mellan Access och Primetime Cloud DRM med ExpressPlay-lösning.
title: Migrera från åtkomst till Multi-DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Migrerar från åtkomst till Multi-DRM {#migrating-from-access-to-multi-drm}

För dem som är bekanta med Adobe Primetime Access DRM-lösningen finns det vissa grundläggande arkitektoniska skillnader mellan Access och Primetime Cloud DRM med ExpressPlay-lösning.

## Arkitekturskillnader mellan åtkomst och multiDRM

|  | Åtkomst | Multi-DRM |
|---|---|---|
| **Paketering** | Packager är bundet till en licensserver. Packager måste känna till den offentliga nyckeln för licensservern när innehållet paketeras. | Packager är inte bundet till en licensserver. |
|  | När innehållet packas är det bundet till en viss licensserver. | Innehållet är inte bundet till en specifik licensserver. En effekt av detta är att du kan paketera allt innehåll innan du får en produktionslicens. |
|  | Packager behöver inte kommunicera med någon form av nyckellagring eftersom nycklarna är säkert inbäddade i själva innehållet (i metadata) efter att de har krypterats. Endast motsvarande licensserver kan läsa dem. | Tangenter måste skickas *till*-paket från ett nyckellagringssystem eller skickas *från* en paketerare till ett nyckellagringssystem. Ett nyckellagringssystem kan antingen vara en kunds eget system, eller så kan det vara ExpressPlays nyckellagringssystem. |
| **Tillstånd** | Klienten begär innehåll till tjänsten Access Cloud. Molntjänsten Access skickar sedan en begäran till kundens tillståndssystem. Kundens tillståndssystem svarar tillbaka med kundens berättiganden. (Klienten har förmodligen fått en cookie för inloggning från kundens servrar innan licensbegäran görs.) | Klienten begär en token från kundens butik (detta är antagligen samma arbetsflöde som kunden tidigare fick en autentiseringscookie). För närvarande utför kunden en kontroll av berättiganden. Om kontrollen av berättiganden lyckas skickar kunden en begäran till ExpressPlay-servrarna för att generera en token för kunden. Denna token är alltid bunden till en viss del av innehållet och *kan* vara bunden till en viss enhet. Kundens butik skickar tillbaka token till klienten. När klienten gör en DRM-uppspelningsbegäran inkluderas token i begäran (metoden för detta är enhetsspecifik) och ExpressPlays DRM-server validerar token utan att anropa kundens server. |