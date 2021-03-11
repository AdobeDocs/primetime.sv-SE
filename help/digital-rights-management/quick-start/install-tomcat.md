---
title: Installera Tomcat
description: Installera Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Installera Tomcat {#install-tomcat}

Du måste installera Tomcat på båda servrarna.
1. Installera Tomcat från katalogen [!DNL \Third Party\Tomcat\6.0.18\] på installations-DVD:n.

   >[!NOTE]
   >
   >Kontrollera att Tomcat är installerat på en plats där det inte finns några blanksteg i sökvägen. Du kan ange `C:\Program Files\Tomcat`, men inte `C:\Tomcat\`.

1. Starta Tomcat genom att ange `TomcatInstallDir>\bin\catalina.bat run`.
1. Gå till startsidan för Tomcat genom att ange `https://<Hostname>:8080/`.
1. Skapa en `crossdomain.xml`-fil och placera filen i katalogen `<TomcatInstallDir>\webapps\ROOT\`.

   Du kan också kopiera en fil från katalogen `https://drmtest2.adobe.com/crossdomain.xml`.
