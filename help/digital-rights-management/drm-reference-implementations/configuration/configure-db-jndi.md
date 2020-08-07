---
description: 'null'
seo-description: 'null'
seo-title: Konfigurera licensserverdatabasen
title: Konfigurera licensserverdatabasen
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Konfigurera licensserverdatabasen{#configure-the-license-server-database}

Så här konfigurerar du exempeldatabasen genom att konfigurera databasschemat och fylla i databasen med exempeldata:

1. Gå upp till kommandoraden för MySQL.

   **I Windows -** Klicka **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **I Linux osv.** - Typ `MySQL`.

1. Kör följande SQL-skript:

   mysql> source &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Det här skriptet lägger till användarkontot `dbuser`, upprättar en anslutning via ett webbprogram och skapar ett databasschema.

   >[!NOTE]
   >
   >Kontrollera att det inte finns något semikolon ( `;`) i slutet av skriptet.

1. Redigera skriptet som fyller i exempeldata i tabellerna för att inkludera data för din testning. `PopulateSampleDB.sql`

   Skriptet finns i `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` mappen.
1. Kör skriptet för att fylla i data som du gjorde i steg 2 [!DNL PopulateSampleDB] .

   >[!NOTE]
   >
   >Första gången du kör skriptet inträffar följande fel: [!DNL CreateSampleDB.sql]

   Du kan ignorera det här felet. Det inträffar bara första gången du kör det här skriptet.

Du måste konfigurera DBCP (Database Connection Pooling), som använder Jakarta-Commons databasanslutningspool. En JNDI-datakälla för TestDB har konfigurerats för att dra nytta av den här anslutningspoolen för programservern. Ändra en av följande filer om du vill ändra databasanslutningen så att den pekar på en MySQL-server som inte finns på localhost:

* Den här [!DNL META-INF\context.xml] filen, som anger plats, användarnamn och lösenord för licensserverns databas som finns i [!DNL flashaccess.war] filen.

* The `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` file.

och återskapa WAR-filen med de uppdaterade filerna.

Om du vill ändra någon av de här parametrarna redigerar du [!DNL context.xml] filen i [!DNL WebContent] katalogen och använder Ant-skriptet för att återskapa WAR-filen. Om du vill justera databasen ändrar du inställningarna för JNDI-datakällan i den här filen.

Om du felsöker Reference Implementation-projektet i Eclipse lägger du till `$CATALINA_HOME\lib\tomcat-dbcp.jar` i din körnings-/felsökningskonfiguration.

>[!NOTE]
>
>Om du kör filen på en fristående Tomcat 6.0-server krävs inte det här steget. [!DNL flashaccess.war]

