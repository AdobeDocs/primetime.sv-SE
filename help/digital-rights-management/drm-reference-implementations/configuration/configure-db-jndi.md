---
title: Konfigurera licensserverdatabasen
description: Konfigurera licensserverdatabasen
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Konfigurera licensserverdatabasen{#configure-the-license-server-database}

Så här konfigurerar du exempeldatabasen genom att konfigurera databasschemat och fylla i databasen med exempeldata:

1. Gå upp till kommandoraden för MySQL.

   **I Windows -** klicka   **[!UICONTROL Window's Start Menu]** >  **[!UICONTROL MySQL]** >  **[!UICONTROL MySQL Server 5.1]** >  **[!UICONTROL MySQL Command Line Client]**

   **I Linux osv.** - Typ  `MySQL`.

1. Kör följande SQL-skript:

   mysql>-källa &quot;`"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Det här skriptet lägger till användarkontot `dbuser`, upprättar en anslutning via ett webbprogram och skapar ett databasschema.

   >[!NOTE]
   >
   >Kontrollera att det inte finns något semikolon ( `;`) i slutet av skriptet.

1. Redigera `PopulateSampleDB.sql`-skriptet som fyller i exempeldata i tabellerna för att inkludera data för din testning.

   Skriptet finns i mappen `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\`.
1. Kör [!DNL PopulateSampleDB]-skriptet för att fylla i data som du gjorde i steg 2.

   >[!NOTE]
   >
   >Första gången du kör skriptet [!DNL CreateSampleDB.sql] inträffar följande fel:

   Du kan ignorera det här felet. Det inträffar bara första gången du kör det här skriptet.

Du måste konfigurera DBCP (Database Connection Pooling), som använder Jakarta-Commons databasanslutningspool. En JNDI-datakälla för TestDB har konfigurerats för att dra nytta av den här anslutningspoolen för programservern. Ändra en av följande filer om du vill ändra databasanslutningen så att den pekar på en MySQL-server som inte finns på localhost:

* Filen [!DNL META-INF\context.xml], som anger plats, användarnamn och lösenord för licensserverns databas som finns i filen [!DNL flashaccess.war].

* Filen `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml`.

och återskapa WAR-filen med de uppdaterade filerna.

Om du vill ändra någon av de här parametrarna redigerar du filen [!DNL context.xml] i katalogen [!DNL WebContent] och använder Ant-skriptet för att återskapa WAR-filen. Om du vill justera databasen ändrar du inställningarna för JNDI-datakällan i den här filen.

Om du felsöker Reference Implementation-projektet i Eclipse lägger du till `$CATALINA_HOME\lib\tomcat-dbcp.jar` i din körnings-/felsökningskonfiguration.

>[!NOTE]
>
>Om du kör filen [!DNL flashaccess.war] på en fristående Tomcat 6.0-server krävs inte det här steget.

