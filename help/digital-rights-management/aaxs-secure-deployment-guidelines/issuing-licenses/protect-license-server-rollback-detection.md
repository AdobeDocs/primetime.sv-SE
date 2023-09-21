---
title: Återställningsigenkänning
description: Återställningsigenkänning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Återställningsigenkänning {#rollback-detection}

Om din implementering av Adobe Access använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om återställningsräknaren inte behövs för implementeringen av Adobe Access kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som erhållits med `MachineToken.getMachineId().getUniqueId()`—och det aktuella räknarvärdet i en databas. Mer information om ökning och spårning av återställningsräknaren finns i ClientState i *API-referens för Adobe Access* och *Återställningsigenkänning* in *Använda Adobe Access SDK för att skydda innehåll*.
