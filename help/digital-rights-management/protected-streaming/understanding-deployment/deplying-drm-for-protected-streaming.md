---
seo-title: Driftsätta Adobe Primetime DRM Server for Protected Streaming
title: Driftsätta Adobe Primetime DRM Server for Protected Streaming
uuid: 83ef8237-0026-4677-b42b-ea4b6de19630
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Distribuera Adobe Primetime DRM-servern för skyddad direktuppspelning{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Innan du kan distribuera Adobe Primetime DRM Server for Protected Streaming måste du ha installerat de versioner av Java och Tomcat som anges i kravavsnittet.

Paketet Primetime DRM Server för skyddad direktuppspelning innehåller [!DNL flashaccesserver.war]. Om du:

* Om du vill distribuera den här WAR-filen måste du kopiera den till Tomcat-katalogen [!DNL webapps].
* Tidigare har du distribuerat WAR-filen. Du kan behöva ta bort den opackade WAR-katalogen ( [!DNL flashaccessserver] i Tomcat&#39;s [!DNL webapps]-katalogen).

* Om du vill förhindra att Tomcat packar upp WAR-filer redigerar du filen [!DNL server.xml] i Tomcat-katalogen [!DNL conf] och konfigurerar attributet `unpackWARs` genom att ange det till `false`.

>[!NOTE]
>
>Om du har konfigurerat Tomcat att inkludera [!DNL commons-logging.jar] i systemklassökvägen (krävs inte för Primetime DRM-servern för skyddad direktuppspelning) måste du konfigurera Commons-log för att använda Log4J.

Servern kan också använda ett plattformsspecifikt bibliotek ( [!DNL jsafe.dll] i Microsoft Windows eller [!DNL libjsafe.so] i Linux för optimala prestanda. Du kan kopiera rätt bibliotek för din plattform från [!DNL thirdparty/cryptoj/]*platform* till en plats som anges av miljövariabeln `PATH` eller `LD_LIBRARY_PATH` i Linux.

>[!NOTE]
>
>Du bör bara använda 64-bitarsversionen om både operativsystemet och JDK har stöd för 64-bitarsversionen. Annars måste du använda 32-bitarsversionen.

