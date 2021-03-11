---
title: Distribuera licensservern och den bevakade mapppaketeraren - översikt
description: Distribuera licensservern och den bevakade mapppaketeraren - översikt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Distribuera licensservern och den bevakade mapppaketeraren - översikt {#deploying-the-license-server-and-watched-folder-packager-overview}

Kopiera licensserverns WAR-filer till Tomcat-katalogen [!DNL webapps]. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort de opackade WAR-katalogerna ( [!DNL flashaccess], [!DNL edcws] och [!DNL flashaccess-packager] i Tomcat-katalogen [!DNL webapps]) manuellt. Om du vill hindra Tomcat från att packa upp WAR-filer redigerar du filen [!DNL server.xml] i Tomcat:s conf-katalog och anger attributet `unpackWARs` till `false`.

Egenskapsfilen ( [!DNL flashaccess-refimpl.properties]) måste finnas i klassökvägen för att servern ska kunna läsa in egenskaperna. Kopiera den här filen till en katalog och uppdatera filen med rätt värden. Redigera filen [!DNL catalina.properties] i Tomcat-katalogen [!DNL conf] och lägg till katalogen som innehåller [!DNL flashaccess-refimpl.properties] i egenskapen `shared.loader`. Filen [!DNL log4j.xml] för konfigurering av loggning måste också finnas i klassökvägen (se [!DNL resources\log4j.xml] som exempel).

Referensimplementeringsservern använder flera certifikatfiler, principfiler och andra resurser. Alla filerna finns i en resursmapp. Som standard är resursmappen [!DNL C:\flashaccess-server-resources], men den här platsen kan ändras i [!DNL flashaccess-refimpl.properties]. Kopiera alla nödvändiga resurser till den här platsen innan du startar servern.

Starta Tomcat och licensservern genom att köra `catalina.bat start` från Tomcat-katalogen [!DNL bin].
