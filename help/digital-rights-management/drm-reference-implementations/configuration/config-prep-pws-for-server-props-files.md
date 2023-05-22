---
title: Förbered lösenord för serveregenskapsfilerna
description: Förbered lösenord för serveregenskapsfilerna
copied-description: true
exl-id: b613d43d-17ec-44e9-bd14-81f9bb9a7f62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Förbered lösenord för serveregenskapsfilerna{#prepare-passwords-for-the-server-properties-files}

Referensimplementeringen innehåller `ScrambleUtil.class`, en klass som garanterar säkerheten för dina autentiseringsuppgifter.

Använd det här verktyget för att kryptera lösenordet innan du tar med det i [!DNL flashaccess-refimpl.properties] -fil.

Om du vill köra verktyget kan du antingen använda ett Ant-skript eller Java.

Verktyget genererar det krypterade lösenordet, som du måste kopiera till [!DNL flashaccess-refimpl.properties] -fil.

>[!NOTE]
>
>Lösenord som har kodats med `ScrambleUtil.class` som har tillhandahållits med referensimplementeringen inte fungerar med Primetime DRM-servern för skyddad direktuppspelning.
