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


# Driftsätta Adobe Primetime DRM Server for Protected Streaming{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Innan du kan distribuera Adobe Primetime DRM Server for Protected Streaming måste du ha installerat de versioner av Java och Tomcat som anges i kravavsnittet.

Paketet Primetime DRM Server for Protected Streaming innehåller [!DNL flashaccesserver.war]. Om du:

* Om du vill distribuera WAR-filen måste du kopiera den till Tomcat- [!DNL webapps] katalogen.
* Tidigare har du distribuerat WAR-filen. Du kan behöva ta bort den opackade WAR-katalogen ( [!DNL flashaccessserver] i Tomcat- [!DNL webapps] katalogen).

* Om du vill förhindra att Tomcat packar upp WAR-filer redigerar du [!DNL server.xml] filen i Tomcat:s [!DNL conf] katalog och konfigurerar `unpackWARs` -attributet genom att ange det som `false`.

>[!NOTE]
>
>Om du har konfigurerat Tomcat så att det finns med [!DNL commons-logging.jar] i klassökvägen System (krävs inte för Primetime DRM Server för skyddad direktuppspelning) måste du konfigurera gemensam loggning så att Log4J används.

Servern kan också använda ett plattformsspecifikt bibliotek ( [!DNL jsafe.dll] i Microsoft Windows eller [!DNL libjsafe.so] i Linux för optimala prestanda. Du kan kopiera rätt bibliotek för din plattform från en [!DNL thirdparty/cryptoj/]*plattform *till en plats som anges av`PATH`systemvariabeln eller`LD_LIBRARY_PATH`i Linux.

>[!NOTE]
>
>Du bör bara använda 64-bitarsversionen om både operativsystemet och JDK har stöd för 64-bitarsversionen. Annars måste du använda 32-bitarsversionen.

