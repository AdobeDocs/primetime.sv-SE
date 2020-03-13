---
seo-title: Använda översikten över klassen DRMErrorEvent
title: Använda översikten över klassen DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Använda översikten över klassen DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime skickar ett `DRMErrorEvent` objekt när ett Primetime-objekt, som försöker spela upp skyddat innehåll, påträffar ett [DRM-relaterat fel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Om inloggningsuppgifterna är ogiltiga skickas objektet upprepade gånger tills användaren anger giltiga inloggningsuppgifter eller tills programmet avvisar fler försök. `DRMAuthenticateEvent` Programmet lyssnar på andra DRM-felhändelser för att upptäcka, identifiera och hantera [DRM-relaterade fel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Även med giltiga inloggningsuppgifter kan villkoren i innehållets licens ändå hindra en användare från att visa det krypterade innehållet. En användare kan till exempel nekas åtkomst om han eller hon försöker visa innehåll i ett obehörigt program (t.ex. programvitlista). Ett obehörigt program är ett program som inte har signerats med ett namnlistat programsigneringscertifikat. I det här fallet skickas ett `DRMErrorEvent` objekt.

Felhändelser kan också utlösas om innehållet är skadat eller om programmets version inte matchar vad licensen anger. Programmet måste ha en lämplig mekanism för att hantera fel.
