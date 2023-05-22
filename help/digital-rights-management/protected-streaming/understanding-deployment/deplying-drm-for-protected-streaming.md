---
title: Driftsätta Adobe Primetime DRM Server for Protected Streaming
description: Driftsätta Adobe Primetime DRM Server for Protected Streaming
copied-description: true
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Driftsätta Adobe Primetime DRM Server for Protected Streaming{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Innan du kan distribuera Adobe Primetime DRM Server for Protected Streaming måste du ha installerat de versioner av Java och Tomcat som anges i kravavsnittet.

Paketet Primetime DRM Server for Protected Streaming innehåller [!DNL flashaccesserver.war]. Om du:

* Vill du distribuera den här WAR-filen måste du kopiera den till Tomcat&#39;s [!DNL webapps] katalog.
* Tidigare har WAR-filen distribuerats, du kan behöva ta bort den opackade WAR-katalogen ( [!DNL flashaccessserver] på Tomcat&#39;s [!DNL webapps] katalog).

* Vill du hindra Tomcat från att packa upp WAR-filer redigerar du [!DNL server.xml] fil i Tomcat&#39;s [!DNL conf] och konfigurera `unpackWARs` genom att ställa in det på `false`.

>[!NOTE]
>
>Om du har konfigurerat Tomcat att inkludera [!DNL commons-logging.jar] i systemklassökvägen (krävs inte för Primetime DRM-servern för skyddad direktuppspelning) måste du konfigurera gemensam loggning så att den använder Log4J.

Servern kan också använda ett plattformsspecifikt bibliotek ( [!DNL jsafe.dll] på Microsoft Windows eller [!DNL libjsafe.so] i Linux för optimala prestanda. Du kan kopiera rätt bibliotek för din plattform från [!DNL thirdparty/cryptoj/]*plattform* till en plats som anges av `PATH` systemvariabel eller `LD_LIBRARY_PATH` i Linux.

>[!NOTE]
>
>Du bör bara använda 64-bitarsversionen om både operativsystemet och JDK har stöd för 64-bitarsversionen. Annars måste du använda 32-bitarsversionen.
