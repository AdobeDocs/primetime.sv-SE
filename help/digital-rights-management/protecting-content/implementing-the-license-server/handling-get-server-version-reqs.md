---
title: Hantera begäranden om hämtning av serverversion
description: Hantera begäranden om hämtning av serverversion
copied-description: true
exl-id: 86a1bbe3-2ae4-4d4e-be51-fbbeb32147c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
