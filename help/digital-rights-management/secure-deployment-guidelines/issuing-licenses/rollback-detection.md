---
description: Om din implementering av Adobe Primetime DRM använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som tillåter listning.
seo-description: Om din implementering av Adobe Primetime DRM använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som tillåter listning.
seo-title: Återställningsigenkänning
title: Återställningsigenkänning
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Återställningsigenkänning {#rollback-detection}

Om din implementering av Adobe Primetime DRM använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som tillåter listning.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om din implementering av Primetime DRM inte kräver återställningsräknaren kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som hämtas med [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())och det aktuella räknarvärdet i en databas.

Mer information om hur du ökar och spårar återställningsräknaren finns i Identifiering av [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) och Rollback.