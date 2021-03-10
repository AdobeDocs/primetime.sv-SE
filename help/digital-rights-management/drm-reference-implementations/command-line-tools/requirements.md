---
title: Krav för kommandoradsverktyg
description: Krav för kommandoradsverktyg
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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