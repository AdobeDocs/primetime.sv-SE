---
title: Distribuera WAR-filer
description: Distribuera WAR-filer
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# Distribuera WAR-filer{#deploy-the-war-files}

1. Kopiera WAR-filen till Tomcat&#39;s [!DNL webapps]-katalogen.

   * Individualiseringsserver: [!DNL flashaccess.war]
   * Nyckelgenereringsserver: [!DNL flashaccess-kgs.war]

1. Kopiera mappen [!DNL ROOT] från paketet som tillhandahålls av Adobe till katalogen [!DNL webapps].

   Individualiseringsservern måste också vara värd för filen [!DNL crossdomain.xml]. (Mappen [!DNL ROOT] innehåller filen [!DNL crossdomain.xml]; [!DNL ROOT] måste vara i versaler.) Nyckelgenereringsservern kräver inte den här filen.

