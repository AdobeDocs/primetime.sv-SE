---
seo-title: Distribuera licensservern och den bevakade mapppaketeraren - översikt
title: Distribuera licensservern och den bevakade mapppaketeraren - översikt
uuid: 4b71f2f4-f971-4382-ae41-171f7dfdfe21
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Distribuera licensservern och den bevakade mapppaketeraren - översikt {#deploying-the-license-server-and-watched-folder-packager-overview}

Kopiera licensserverns WAR-filer till Tomcat- [!DNL webapps] katalogen. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort de opackade WAR-katalogerna ( [!DNL flashaccess], [!DNL edcws]och [!DNL flashaccess-packager] i Tomcat- [!DNL webapps] katalogen) manuellt. Om du vill hindra Tomcat från att packa upp WAR-filer redigerar du filen i Tomcat-katalogen och anger [!DNL server.xml] attributet till `unpackWARs` `false`.

Egenskapsfilen ( [!DNL flashaccess-refimpl.properties]) måste finnas i klassökvägen för att servern ska kunna läsa in egenskaperna. Kopiera den här filen till en katalog och uppdatera filen med rätt värden. Redigera [!DNL catalina.properties] filen i Tomcat:s [!DNL conf] katalog och lägg till katalogen som innehåller [!DNL flashaccess-refimpl.properties] i `shared.loader` egenskapen. Filen som [!DNL log4j.xml] konfigurerar loggning måste också finnas i klassökvägen (se [!DNL resources\log4j.xml] ett exempel).

Referensimplementeringsservern använder flera certifikatfiler, principfiler och andra resurser. Alla filerna finns i en resursmapp. Som standard är resursmappen [!DNL C:\flashaccess-server-resources]men den här platsen kan ändras i [!DNL flashaccess-refimpl.properties]. Kopiera alla nödvändiga resurser till den här platsen innan du startar servern.

Starta Tomcat och licensservern genom att köra `catalina.bat start` från Tomcat- [!DNL bin] katalogen.
