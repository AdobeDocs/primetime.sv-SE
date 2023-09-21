---
title: Förbered lösenord för serveregenskapsfilerna
description: Förbered lösenord för serveregenskapsfilerna
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
>Lösenord som har kodats med `ScrambleUtil.class` som har tillhandahållits med referensimplementeringen inte fungerar med Primetime DRM-servern för skyddad strömning.
