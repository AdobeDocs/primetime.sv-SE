---
title: Hantera begäranden om hämtning av serverversion
description: Hantera begäranden om hämtning av serverversion
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Hantera begäranden om hämtning av serverversion {#handle-get-server-version-requests}

Adobe Primetime DRM client 3.0 eller senare skickar en Get Server Version-förfrågan för att fastställa serverns funktioner. Alla servrar som använder Primetime DRM SDK 3.0 eller senare måste implementera stöd för begäranden om Get Server-version.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* Begärans URL måste vara &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

För Primetime DRM SDK 4.0 eller senare anger svaret på en Get Server Version-begäran för klienterna att servern stöder version 3 och 4 av Primetime DRM-protokollet.
