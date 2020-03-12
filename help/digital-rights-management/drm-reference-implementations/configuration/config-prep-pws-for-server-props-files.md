---
description: 'null'
seo-description: 'null'
seo-title: Förbered lösenord för serveregenskapsfilerna
title: Förbered lösenord för serveregenskapsfilerna
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Förbered lösenord för serveregenskapsfilerna{#prepare-passwords-for-the-server-properties-files}

Referensimplementeringen innehåller `ScrambleUtil.class`en klass som garanterar säkerheten för dina autentiseringsuppgifter.

Använd det här verktyget för att kryptera lösenordet innan du tar med det i [!DNL flashaccess-refimpl.properties] filen.

Om du vill köra verktyget kan du antingen använda ett Ant-skript eller Java.

Verktyget genererar det krypterade lösenordet, som du måste kopiera till [!DNL flashaccess-refimpl.properties] filen.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Lösenord som har kodats med det `ScrambleUtil.class` som har angetts i referensimplementeringen fungerar inte med Primetime DRM-servern för skyddad direktuppspelning.
