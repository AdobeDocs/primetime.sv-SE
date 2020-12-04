---
seo-title: Distribuera Adobe Access Server för skyddad strömning - översikt
title: Distribuera Adobe Access Server för skyddad strömning - översikt
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Distribuera Adobe Access Server för skyddad strömning - översikt {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Innan du distribuerar Adobe Access Server för skyddad strömning måste du kontrollera att du har installerat de versioner av Java och Tomcat som listas i avsnittet Krav.

Paketet Adobe Access Server för skyddad strömning innehåller [!DNL flashaccesserver.war]. Om du vill distribuera WAR-filen kopierar du den till Tomcat-katalogen [!DNL webapps]. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort den opackade WAR-katalogen ( [!DNL flashaccessserver] i Tomcat&#39;s [!DNL webapps]-katalogen) manuellt. Om du vill hindra Tomcat från att packa upp WAR-filer redigerar du filen [!DNL server.xml] i Tomcat-katalogen [!DNL conf] och anger attributet `unpackWARs` till `false`.

>[!NOTE]
>
>Om du har konfigurerat Tomcat att inkludera [!DNL commons-logging.jar] i systemklassökvägen (krävs inte för Adobe Access Server för skyddad direktuppspelning), måste Commons-log vara konfigurerad att använda Log4J.

Servern kan också använda ett plattformsspecifikt bibliotek ( [!DNL jsafe.dll] i Microsoft Windows eller [!DNL libjsafe.so] i Linux) för optimala prestanda. Kopiera rätt bibliotek för din plattform från [!DNL thirdparty/cryptoj/]*plattform* till en plats som anges av miljövariabeln `PATH` (eller `LD_LIBRARY_PATH` i Linux).

>[!NOTE]
>
>64-bitarsversionen bör bara användas om både operativsystemet och JDK har stöd för 64-bitarsversionen, annars används 32-bitarsversionen.

