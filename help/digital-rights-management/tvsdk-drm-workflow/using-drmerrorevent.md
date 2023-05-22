---
title: Använda översikten över klassen DRMErrorEvent
description: Använda översikten över klassen DRMErrorEvent
copied-description: true
exl-id: c651cdcf-f8f8-4085-a88e-d82030f90f11
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Använda klassen DRMErrorEvent {#using-the-drmerrorevent-class}

Primetime skickar en `DRMErrorEvent` när ett Primetime-objekt försöker spela upp skyddat innehåll påträffar ett [DRM-relaterat fel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Om inloggningsuppgifterna är ogiltiga visas `DRMAuthenticateEvent` -objektet skickas upprepade gånger tills användaren anger giltiga inloggningsuppgifter eller tills programmet avvisar fler försök. Programmet lyssnar på andra DRM-felhändelser för att upptäcka, identifiera och hantera [DRM-relaterade fel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Även med giltiga inloggningsuppgifter kan villkoren i innehållets licens ändå hindra en användare från att visa det krypterade innehållet. En användare kan till exempel nekas åtkomst om han eller hon försöker visa innehåll i ett obehörigt program (t.ex. listan över tillåtna program). Ett obehörigt program är ett program som inte har signerats med ett godkänt signeringscertifikat för program i listan. I det här fallet `DRMErrorEvent` -objektet skickas.

Felhändelser kan också utlösas om innehållet är skadat eller om programmets version inte matchar vad licensen anger. Programmet måste ha en lämplig mekanism för att hantera fel.

## Skapa en DRMErrorEvent-hanterare {#create-a-drmerrorevent-handler}

Skapa en händelsehanterare för att bearbeta felhändelser som skickas från Primetime när ett fel påträffas när skyddat innehåll spelas upp.

När ett program påträffar ett fel utförs vanligtvis ett antal rensningsåtgärder. Därefter informeras användaren om felet och användaren får alternativ för att lösa problemet.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
