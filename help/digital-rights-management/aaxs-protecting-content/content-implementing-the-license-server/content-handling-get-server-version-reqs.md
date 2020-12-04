---
seo-title: Hantera begäranden om hämtning av serverversion
title: Hantera begäranden om hämtning av serverversion
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Hantera begäranden om hämtning av serverversion{#handling-get-server-version-requests}

Adobe Access client 3.0 och senare skickar en Get Server Version-begäran för att fastställa serverns funktioner. Alla servrar som använder Adobe Access SDK 3.0 eller senare måste ha stöd för Get Server Version-begäranden.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* Begärans URL måste vara &quot;License Server URL in metadata&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

För Adobe Access SDK 4.0 och senare anger svaret på en Get Server Version-begäran att servern stöder version 3 och 4 av Adobe Access-protokollet.
