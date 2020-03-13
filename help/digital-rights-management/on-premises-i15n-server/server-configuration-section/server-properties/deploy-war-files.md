---
seo-title: Distribuera WAR-filer
title: Distribuera WAR-filer
uuid: 435a6a6e-c981-46fb-bca9-7f5f34eecd6a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Distribuera WAR-filer{#deploy-the-war-files}

1. Kopiera WAR-filen till Tomcat- [!DNL webapps] katalogen.

   * Individualiseringsserver: [!DNL flashaccess.war]
   * Nyckelgenereringsserver: [!DNL flashaccess-kgs.war]

1. Kopiera mappen från det paket som Adobe tillhandahåller till [!DNL ROOT] [!DNL webapps] katalogen.

   Individualiseringsservern måste också vara värd för [!DNL crossdomain.xml] filen. (Mappen [!DNL ROOT] innehåller [!DNL crossdomain.xml] filen; [!DNL ROOT] måste vara i versaler.) Nyckelgenereringsservern kräver inte den här filen.

