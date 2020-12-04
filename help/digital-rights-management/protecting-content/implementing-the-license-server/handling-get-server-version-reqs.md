---
seo-title: Hantera begäranden om hämtning av serverversion
title: Hantera begäranden om hämtning av serverversion
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Hantera begäranden om hämtning av serverversion {#handle-get-server-version-requests}

Adobe Primetime DRM client 3.0 eller senare skickar en Get Server Version-förfrågan för att fastställa serverns funktioner. Alla servrar som använder Primetime DRM SDK 3.0 eller senare måste implementera stöd för begäranden om Get Server-version.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* Begärans URL måste vara &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

För Primetime DRM SDK 4.0 eller senare anger svaret på en Get Server Version-begäran för klienterna att servern stöder version 3 och 4 av Primetime DRM-protokollet.
