---
description: 'null'
seo-description: 'null'
seo-title: Konfigurera licensserverdatabasen
title: Konfigurera licensserverdatabasen
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '219'
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

1. Gå till [!DNL Third Party\MySQL\Installer\5.1] mappen på dvd-skivan och starta installationsprogrammet.
1. Slutför MySQL-installationen.
1. Välj **[!UICONTROL Configure MySQL Server Now]** att starta konfigurationsguiden.
1. Använd standardinställningarna eller välj specifika inställningar för testningen tills den femte skärmen visas.
1. På den femte skärmen väljer **[!UICONTROL Online Transaction Processing (OLTP)]** eller **[!UICONTROL Manual Setting]** anger du det maximala antalet tillåtna anslutningar.
1. Skriv ned rotlösenordet.
1. Så här installerar du om MySQL om du behöver starta servern senare:
   1. Ta bort *systemenheten:* mapp.

      Mappen finns i [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. Ta bort den gamla installationsmappen för MySQL.

      Exempel: *systemenhet:*, som finns i [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. Om du vill installera MySQL JDBC Driver 5.1.7 kopierar du [!DNL mysql-connector-java-5.1.7-bin.jar] filen i [!DNL Third Party\MySQL\Installer\5.1] -mappen på dvd-skivan till [!DNL ...\Tomcat6.0\lib] katalogen på Tomcat-servern.

   >[!NOTE]
   >
   >MySQL JDBC Driver 5.1.7 fungerar med Tomcat 6.0. Äldre versioner av Tomcat stöds inte längre.

