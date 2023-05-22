---
title: Förgenererande licenser
description: Förgenererande licenser
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Förgenererande licenser{#pre-generating-licenses}

Om du förgenererar licenser som innehåller tidsbaserade användningsregler rekommenderar vi att licensen innehåller synkroniseringskrav (se *Använda Adobe Access SDK för att skydda innehåll* så att licensens förfallodatum kan framtvingas på ett säkert sätt. Vi rekommenderar att du implementerar en&quot;hjärttaktmekanism&quot; mellan klienten och servern om du har tidsbaserade begränsningar i licensen, eftersom hjärtslagen synkroniserar klienttiden med servertiden.
