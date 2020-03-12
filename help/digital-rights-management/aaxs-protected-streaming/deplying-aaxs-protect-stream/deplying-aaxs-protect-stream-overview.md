---
seo-title: Distribuera Adobe Access Server for Protected Streaming - översikt
title: Distribuera Adobe Access Server for Protected Streaming - översikt
uuid: 48a7e452-520a-4ff8-97e9-11210221256d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Distribuera Adobe Access Server for Protected Streaming - översikt {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Innan du distribuerar Adobe Access Server for Protected Streaming måste du kontrollera att du har installerat de versioner av Java och Tomcat som listas i avsnittet Krav.

Paketet Adobe Access Server for Protected Streaming innehåller [!DNL flashaccesserver.war]. Om du vill distribuera WAR-filen kopierar du den till Tomcat- [!DNL webapps] katalogen. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort den opackade WAR-katalogen ( [!DNL flashaccessserver] i Tomcat- [!DNL webapps] katalogen) manuellt. Om du vill hindra Tomcat från att packa upp WAR-filer redigerar du [!DNL server.xml] filen i Tomcat:s [!DNL conf] katalog och anger `unpackWARs` attributet till `false`.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om du har konfigurerat Tomcat så att det finns med [!DNL commons-logging.jar] i klassökvägen System (krävs inte för Adobe Access Server for Protected Streaming), måste Commons-log vara konfigurerad att använda Log4J.

Servern kan också använda ett plattformsspecifikt bibliotek ( [!DNL jsafe.dll] i Microsoft Windows eller [!DNL libjsafe.so] i Linux) för optimala prestanda. Kopiera rätt bibliotek för din plattform från en [!DNL thirdparty/cryptoj/]*plattform *till en plats som anges av`PATH`systemvariabeln (eller`LD_LIBRARY_PATH`i Linux).

>[!NOTE] {class=&quot;- topic/note &quot;
>
>64-bitarsversionen bör bara användas om både operativsystemet och JDK har stöd för 64-bitarsversionen, annars används 32-bitarsversionen.

