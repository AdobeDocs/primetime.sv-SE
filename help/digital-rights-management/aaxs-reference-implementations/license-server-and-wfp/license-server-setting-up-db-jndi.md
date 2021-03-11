---
title: Konfigurera databasen och konfigurera JNDI-datakällan
description: Konfigurera databasen och konfigurera JNDI-datakällan
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Konfigurera databasen och konfigurera JNDI-datakällan {#setting-up-the-database-and-configuring-the-jndi-datasource}

Referensimplementeringslicensservern kräver en databas som stöder följande funktioner:

* Användarautentisering
* Affärsregler för demonstration av användningsmodell
* Konvertering av metadata
* Domänstöd

Anonym licensköp kräver inte att en databas körs.

>[!NOTE]
>
>Instruktionerna i det här avsnittet gäller Microsoft Windows-plattformen. Andra operativsystem hittar du i dokumentationen för ditt operativsystem eller i MySQL-dokumentationen.

Om du vill köra licensservern måste du installera och konfigurera MySQL 5.1.34:

1. Kör MySQL-installationsprogrammet (finns i den tredje Party\MySQL\Installer\5.1-mappen på dvd-skivan).
1. När du är klar med installationen startar du konfigurationsguiden genom att kontrollera **[!UICONTROL Configure MySQL Server Now]**. Använd standardinställningarna eller välj specifika inställningar för testningen, med undantag för att du på den femte skärmen måste välja **[!UICONTROL Online Transaction Processing (OLTP)]** eller **[!UICONTROL Manual Setting]** och ange maximalt antal tillåtna anslutningar.

1. Notera rotlösenordet.
1. Om du behöver installera om MySQL följer du de här stegen för att undvika problem med att starta servern efteråt:

   * Ta bort mappen *systemenhet:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * Ta bort den gamla installationsmappen för MySQL: till exempel *systemenhet:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

Därefter måste du installera MySQL JDBC Driver 5.1.7. Det gör du genom att kopiera [!DNL mysql-connector-java-5.1.7-bin.jar] (finns i mappen [!DNL Third Party\MySQL\Installer\5.1] på dvd-skivan) till Tomcat Server lib-katalogen: [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC Driver 5.1.7 fungerar med Tomcat 6.0. Äldre versioner av Tomcat stöds inte.

Konfigurera exempeldatabasen genom att konfigurera databasschemat och fylla i databasen med exempeldata. Gör så här:

1. Gå till **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**.
1. När du har angett lösenordet kör du följande SQL-skript för att lägga till användarkontot `dbuser` för att upprätta en anslutning via ett webbprogram och skapa databasschema (se till att det inte finns något&quot;;&quot; i slutet). Tryck bara på Retur.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. Redigera skriptet som fyller i exempeldata i tabellerna för att inkludera data i testsyfte: [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. Kör det här skriptet för att fylla i data som du gjorde i steg 2.

>[!NOTE]
>
>Första gången du kör [!DNL CreateSampleDB.sql]-skriptet får du följande fel:

*FEL 1396 (HY000): Åtgärden DROP USER misslyckades för frågan dbuser@&#39;localhost&#39; OK, 0 rader påverkades (0,00 sek).*

Du kan ignorera det här felet. Detta händer bara första gången du kör skriptet.

Nu måste du konfigurera DBCP (Database Connection Pooling). DBCP använder Jakarta-Commons databasanslutningspool. En JNDI-datakälla för TestDB har konfigurerats för att dra nytta av den här anslutningspoolen för programservern. Om du vill ändra databasanslutningen till att peka på en MySQL-server som inte finns på en lokal värd ändrar du filen [!DNL META-INF\context.xml] (som anger plats, användarnamn och lösenord för licensserverns databas) som finns i [!DNL flashaccess.war], eller ändrar [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] och återskapar WAR-filen med de uppdaterade filerna. Om du vill ändra någon av de här parametrarna redigerar du [!DNL context.xml] som finns i WebContent-katalogen och använder Ant-skriptet för att återskapa WAR-filen. Om du vill justera databasen ändrar du inställningarna för JNDI-datakällan i den här filen.

Om du felsöker Reference Implementation-projektet i Eclipse måste du lägga till `$CATALINA_HOME\lib\tomcat-dbcp.jar` i körnings-/felsökningskonfigurationen. Det här steget krävs inte om du kör filen [!DNL flashaccess.war] på en fristående Tomcat 6.0-server.
