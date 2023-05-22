---
title: Krav för kommandoradsverktyg
description: Krav för kommandoradsverktyg
copied-description: true
exl-id: b19512d0-0865-4c24-a6d8-1f26cd3f210c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 0%

---

# Krav för kommandoradsverktyg {#command-line-tools-requirements}

* Java 1.5 eller senare.
* Autentiseringsuppgifter för Packager, transport och licensserver (certifikat och lösenord) som utfärdas av Adobe.

   Det här är autentiseringsuppgifter som används för att kryptera och signera videofiler, för att signera principuppdaterings- och återkallningslistor och för att generera licenser i förväg.

>[!NOTE]
>
>På grund av ett Java-fel kan alla argument som du skriver på kommandoraden (t.ex. filnamn, DRM-principnamn eller beskrivningar) bara använda tecken från operativsystemets standardteckenuppsättning.
