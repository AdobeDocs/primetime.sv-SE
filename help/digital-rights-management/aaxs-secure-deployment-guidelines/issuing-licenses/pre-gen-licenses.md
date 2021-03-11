---
title: Förgenererande licenser
description: Förgenererande licenser
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Förgenererande licenser{#pre-generating-licenses}

Om du förgenererar licenser som innehåller tidsbaserade användningsregler rekommenderar vi att licensen innehåller synkroniseringskrav (se *Använda Adobe Access SDK för att skydda innehåll*-guiden), så att licensens förfallodatum kan framtvingas på ett säkert sätt. Vi rekommenderar att du implementerar en&quot;hjärttaktmekanism&quot; mellan klienten och servern om du har tidsbaserade begränsningar i licensen, eftersom hjärtslagen synkroniserar klienttiden med servertiden.
