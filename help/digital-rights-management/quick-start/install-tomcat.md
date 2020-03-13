---
seo-title: Installera Tomcat
title: Installera Tomcat
uuid: f7663eda-ad18-4a6e-bb9f-01c74721b047
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Installera Tomcat {#install-tomcat}

Du måste installera Tomcat på båda servrarna.
1. Installera Tomcat från katalogen [!DNL \Third Party\Tomcat\6.0.18\] på installations-DVD:n.

   >[!NOTE]
   >
   >Kontrollera att Tomcat är installerat på en plats där det inte finns några blanksteg i sökvägen. Du kan skriva `C:\Program Files\Tomcat`in, men inte `C:\Tomcat\`.

1. Starta Tomcat genom att skriva `TomcatInstallDir>\bin\catalina.bat run`.
1. Gå till startsidan för Tomcat genom att gå in `https://<Hostname>:8080/`.
1. Skapa en `crossdomain.xml` fil och placera filen i `<TomcatInstallDir>\webapps\ROOT\` katalogen.

   Du kan också kopiera en fil från `https://drmtest2.adobe.com/crossdomain.xml` katalogen.
