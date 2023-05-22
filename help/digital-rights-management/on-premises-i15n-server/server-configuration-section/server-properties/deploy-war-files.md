---
title: Distribuera WAR-filer
description: Distribuera WAR-filer
copied-description: true
exl-id: 9f491596-2a02-4a55-9baa-86407e389d20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---

# Distribuera WAR-filer{#deploy-the-war-files}

1. Kopiera WAR-filen till Tomcat&#39;s [!DNL webapps] katalog.

   * Individualiseringsserver: [!DNL flashaccess.war]
   * Nyckelgenereringsserver: [!DNL flashaccess-kgs.war]

1. Kopiera [!DNL ROOT] från det paket som Adobe tillhandahåller till [!DNL webapps] katalog.

   Individualiseringsservern måste också vara värd för [!DNL crossdomain.xml] -fil. (Med [!DNL ROOT] mappen innehåller [!DNL crossdomain.xml] fil, [!DNL ROOT] måste vara i versaler.) Nyckelgenereringsservern kräver inte den här filen.
