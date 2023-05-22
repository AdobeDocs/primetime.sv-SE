---
title: Distribuera licensservern och den bevakade mapppaketeraren - översikt
description: Distribuera licensservern och den bevakade mapppaketeraren - översikt
copied-description: true
exl-id: b44aec8b-f1d7-4dce-bc51-0ce2b74ae0c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Distribuera licensservern och den bevakade mapppaketeraren - översikt {#deploying-the-license-server-and-watched-folder-packager-overview}

Kopiera licensserverns WAR-filer till Tomcat&#39;s [!DNL webapps] katalog. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort de opackade WAR-katalogerna manuellt ( [!DNL flashaccess], [!DNL edcws]och [!DNL flashaccess-packager] på Tomcat&#39;s [!DNL webapps] katalog). Om du vill förhindra att Tomcat packar upp WAR-filer redigerar du [!DNL server.xml] filen i Tomcat&#39;s conf directory och ange `unpackWARs` attribut till `false`.

Egenskapsfilen ( [!DNL flashaccess-refimpl.properties]) måste finnas i klassökvägen för att servern ska kunna läsa in egenskaperna. Kopiera den här filen till en katalog och uppdatera filen med rätt värden. Redigera [!DNL catalina.properties] fil i Tomcat&#39;s [!DNL conf] och lägga till katalogen som innehåller [!DNL flashaccess-refimpl.properties] till `shared.loader` -egenskap. The [!DNL log4j.xml] filen för konfigurering av loggning måste också finnas i klassökvägen (se [!DNL resources\log4j.xml] till exempel).

Referensimplementeringsservern använder flera certifikatfiler, principfiler och andra resurser. Alla filerna finns i en resursmapp. Som standard är resursmappen [!DNL C:\flashaccess-server-resources]men den här platsen kan ändras i [!DNL flashaccess-refimpl.properties]. Kopiera alla nödvändiga resurser till den här platsen innan du startar servern.

Starta Tomcat och licensservern genom att köra `catalina.bat start` från Tomcat&#39;s [!DNL bin] katalog.
