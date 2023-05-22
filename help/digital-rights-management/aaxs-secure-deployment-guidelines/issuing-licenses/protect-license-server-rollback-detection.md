---
title: Återställningsigenkänning
description: Återställningsigenkänning
copied-description: true
exl-id: 054d3634-5ce9-4a51-ac91-e6ae60a1fd6e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Återställningsigenkänning {#rollback-detection}

Om din implementering av Adobe Access använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om återställningsräknaren inte behövs för implementeringen av Adobe Access kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som erhållits med `MachineToken.getMachineId().getUniqueId()`—och det aktuella räknarvärdet i en databas. Mer information om ökning och spårning av återställningsräknaren finns i ClientState i *API-referens för Adobe Access* och *Återställningsigenkänning* in *Använda Adobe Access SDK för att skydda innehåll*.
