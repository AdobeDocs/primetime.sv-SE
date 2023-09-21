---
title: Installera Tomcat
description: Installera Tomcat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Installera Tomcat {#install-tomcat}

Du måste installera Tomcat på båda servrarna.
1. Installera Tomcat från [!DNL \Third Party\Tomcat\6.0.18\] katalog på installations-DVD:n.

   >[!NOTE]
   >
   >Kontrollera att Tomcat är installerat på en plats där det inte finns några blanksteg i sökvägen. Du kan skriva `C:\Program Files\Tomcat`, men inte `C:\Tomcat\`.

1. Starta Tomcat genom att ange `TomcatInstallDir>\bin\catalina.bat run`.
1. Gå till startsidan för Tomcat och gå till startsidan för att kontrollera installationen. `https://<Hostname>:8080/`.
1. Skapa en `crossdomain.xml` och montera filen i `<TomcatInstallDir>\webapps\ROOT\` katalog.

   Du kan även kopiera en fil från `https://drmtest2.adobe.com/crossdomain.xml` katalog.
