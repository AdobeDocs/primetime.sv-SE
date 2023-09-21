---
title: Konfigurera licensserverdatabasen
description: Konfigurera licensserverdatabasen
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Konfigurera licensserverdatabasen{#set-up-the-license-server-database}

Referensimplementeringslicensservern kräver en databas som stöder följande:

* Användarautentisering
* Affärsregler för demonstration av användningsmodell
* Konvertering av metadata
* Domänstöd

Anonym licensköp kräver inte att databasen körs.

>[!NOTE]
>
>Den här proceduren gäller endast Microsoft Windows. Andra operativsystem hittar du i dokumentationen för ditt operativsystem eller i MySQL-dokumentationen.

Om du vill köra licensservern måste du installera och konfigurera MySQL:

1. På DVD:n går du till [!DNL Third Party\MySQL\Installer\5.1] och starta installationsprogrammet.
1. Slutför MySQL-installationen.
1. Välj **[!UICONTROL Configure MySQL Server Now]** för att starta konfigurationsguiden.
1. Använd standardinställningarna eller välj specifika inställningar för testningen tills den femte skärmen visas.
1. På femte skärmen väljer du **[!UICONTROL Online Transaction Processing (OLTP)]** eller **[!UICONTROL Manual Setting]** och ange maximalt antal tillåtna anslutningar.
1. Skriv ned rotlösenordet.
1. Så här installerar du om MySQL om du behöver starta servern senare:
   1. Ta bort *systemenhet:* mapp.

      Mappen finns i [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Ta bort den gamla installationsmappen för MySQL.

      Till exempel: *systemenhet:* som finns i [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Om du vill installera MySQL JDBC Driver 5.1.7 kopierar du [!DNL mysql-connector-java-5.1.7-bin.jar] i [!DNL Third Party\MySQL\Installer\5.1] på dvd-skivan till [!DNL ...\Tomcat6.0\lib] på Tomcat Server.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 fungerar med Tomcat 6.0. Äldre versioner av Tomcat stöds inte längre.
