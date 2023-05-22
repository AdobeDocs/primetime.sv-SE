---
title: Konfigurera licensserverdatabasen
description: Konfigurera licensserverdatabasen
copied-description: true
exl-id: 1d5d988e-d22a-4405-8f39-1763f1f65094
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Konfigurera licensserverdatabasen{#configure-the-license-server-database}

Så här konfigurerar du exempeldatabasen genom att konfigurera databasschemat och fylla i databasen med exempeldata:

1. Gå upp till kommandoraden för MySQL.

   **I Windows -** Klicka  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **I Linux osv.** - Typ `MySQL`.

1. Kör följande SQL-skript:

   mysql> källa &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   Det här skriptet lägger till användarkontot `dbuser`skapar en anslutning via ett webbprogram och skapar ett databasschema.

   >[!NOTE]
   >
   >Kontrollera att det inte finns något semikolon ( `;`) i slutet av skriptet.

1. Redigera `PopulateSampleDB.sql` skript som fyller i exempeldata i tabellerna för att inkludera data för din testning.

   Skriptet finns i `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` mapp.
1. Kör [!DNL PopulateSampleDB] skript för att fylla i data som du gjorde i steg 2.

   >[!NOTE]
   >
   >Första gången du kör [!DNL CreateSampleDB.sql] skript: följande fel inträffar:

   Du kan ignorera det här felet. Det inträffar bara första gången du kör det här skriptet.

Du måste konfigurera DBCP (Database Connection Pooling), som använder Jakarta-Commons databasanslutningspool. En JNDI-datakälla för TestDB har konfigurerats för att dra nytta av den här anslutningspoolen för programservern. Ändra en av följande filer om du vill ändra databasanslutningen så att den pekar på en MySQL-server som inte finns på localhost:

* The [!DNL META-INF\context.xml] som anger plats, användarnamn och lösenord för licensserverns databas som finns i [!DNL flashaccess.war] -fil.

* The `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` -fil.

och återskapa WAR-filen med de uppdaterade filerna.

Om du vill ändra någon av de här parametrarna redigerar du [!DNL context.xml] i [!DNL WebContent] och använd Ant-skriptet för att återskapa WAR-filen. Om du vill justera databasen ändrar du inställningarna för JNDI-datakällan i den här filen.

Om du felsöker Reference Implementation-projektet i Eclipse lägger du till `$CATALINA_HOME\lib\tomcat-dbcp.jar` till din körnings-/felsökningskonfiguration.

>[!NOTE]
>
>Om du kör [!DNL flashaccess.war] på en fristående Tomcat 6.0-server krävs inte det här steget.
