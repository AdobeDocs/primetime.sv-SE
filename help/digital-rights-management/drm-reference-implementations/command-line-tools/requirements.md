---
title: Krav för kommandoradsverktyg
description: Krav för kommandoradsverktyg
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
