---
description: Om din implementering av Adobe Primetime DRM använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som Tillåt listning.
title: Återställningsigenkänning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Återställningsidentifiering {#rollback-detection}

Om din implementering av Adobe Primetime DRM använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som Tillåt listning.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om din implementering av Primetime DRM inte kräver återställningsräknaren kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som hämtas med [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) och det aktuella räknarvärdet i en databas.

Mer information om hur du ökar och spårar återställningsräknaren finns i [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) och Återställningsidentifiering.