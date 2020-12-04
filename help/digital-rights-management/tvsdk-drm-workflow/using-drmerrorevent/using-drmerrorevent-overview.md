---
seo-title: Använda översikten över klassen DRMErrorEvent
title: Använda översikten över klassen DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Använda översikten över klassen DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime skickar ett `DRMErrorEvent`-objekt när ett Primetime-objekt försöker spela upp skyddat innehåll och påträffar ett [DRM-relaterat fel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Om inloggningsuppgifterna är ogiltiga skickas `DRMAuthenticateEvent`-objektet upprepade gånger tills användaren anger giltiga inloggningsuppgifter eller tills programmet nekar fler försök. Programmet lyssnar på andra DRM-felhändelser för att upptäcka, identifiera och hantera [DRM-relaterade fel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Även med giltiga inloggningsuppgifter kan villkoren i innehållets licens ändå hindra en användare från att visa det krypterade innehållet. En användare kan till exempel nekas åtkomst om han eller hon försöker visa innehåll i ett obehörigt program (t.ex. listan över tillåtna program). Ett obehörigt program är ett program som inte har signerats med ett godkänt signeringscertifikat för program i listan. I det här fallet skickas ett `DRMErrorEvent`-objekt.

Felhändelser kan också utlösas om innehållet är skadat eller om programmets version inte matchar vad licensen anger. Programmet måste ha en lämplig mekanism för att hantera fel.
