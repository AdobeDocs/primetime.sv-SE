---
title: Distribuera Adobe Access Server för skyddad strömning - översikt
description: Distribuera Adobe Access Server för skyddad strömning - översikt
copied-description: true
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Distribuera Adobe Access Server för skyddad strömning - översikt {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Innan du distribuerar Adobe Access Server för skyddad strömning måste du kontrollera att du har installerat de versioner av Java och Tomcat som listas i avsnittet Krav.

Paketet Adobe Access Server för skyddad strömning innehåller [!DNL flashaccesserver.war]. Om du vill distribuera WAR-filen kopierar du den till Tomcat&#39;s [!DNL webapps] katalog. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort den packade WAR-katalogen manuellt ( [!DNL flashaccessserver] på Tomcat&#39;s [!DNL webapps] katalog). Om du vill förhindra att Tomcat packar upp WAR-filer redigerar du [!DNL server.xml] fil i Tomcat&#39;s [!DNL conf] och ange `unpackWARs` attribut till `false`.

>[!NOTE]
>
>Om du har konfigurerat Tomcat att inkludera [!DNL commons-logging.jar] i systemklassökvägen (krävs inte för Adobe Access Server för skyddad direktuppspelning) måste gemensam loggning konfigureras för att använda Log4J.

Servern kan också använda ett plattformsspecifikt bibliotek ( [!DNL jsafe.dll] på Microsoft Windows eller [!DNL libjsafe.so] i Linux) för optimala prestanda. Kopiera rätt bibliotek för din plattform från [!DNL thirdparty/cryptoj/]*plattform* till en plats som anges av `PATH` miljövariabel (eller `LD_LIBRARY_PATH` i Linux).

>[!NOTE]
>
>64-bitarsversionen bör bara användas om både operativsystemet och JDK har stöd för 64-bitarsversionen, annars används 32-bitarsversionen.
