---
seo-title: Distribuera WAR-filer
title: Distribuera WAR-filer
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
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

