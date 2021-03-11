---
title: Förbered lösenord för serveregenskapsfilerna
description: Förbered lösenord för serveregenskapsfilerna
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# Förbered lösenord för serveregenskapsfilerna{#prepare-passwords-for-the-server-properties-files}

Referensimplementeringen innehåller `ScrambleUtil.class`, en klass som garanterar säkerheten för dina autentiseringsuppgifter.

Använd det här verktyget för att kryptera lösenordet innan du tar med det i [!DNL flashaccess-refimpl.properties]-filen.

Om du vill köra verktyget kan du antingen använda ett Ant-skript eller Java.

Verktyget genererar det krypterade lösenordet, som du måste kopiera till filen [!DNL flashaccess-refimpl.properties].

>[!NOTE]
>
>Lösenord som har kodats med `ScrambleUtil.class` som har angetts med referensimplementeringen fungerar inte med Primetime DRM-servern för skyddad direktuppspelning.
