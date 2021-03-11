---
description: DRMAuthenticateEvent-objektet skickas när ett Primetime-objekt försöker att spela upp skyddat innehåll som kräver inloggningsuppgifter för autentisering innan uppspelning (och autentisering ännu inte har utförts). DRMAuthenticateEvent-hanteraren samlar in de inloggningsuppgifter som krävs (användarnamn, lösenord och typ) och skickar värdena till .setDRMAuthenticationCredentials()-metoden för validering.
title: Skapa en DRMAuthenticateEvent-hanterare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Skapa en DRMAuthenticateEvent-hanterare{#create-a-drmauthenticateevent-handler}

DRMAuthenticateEvent-objektet skickas när ett Primetime-objekt försöker att spela upp skyddat innehåll som kräver inloggningsuppgifter för autentisering innan uppspelning (och autentisering ännu inte har utförts). DRMAuthenticateEvent-hanteraren samlar in de inloggningsuppgifter som krävs (användarnamn, lösenord och typ) och skickar värdena till .setDRMAuthenticationCredentials()-metoden för validering.

Programmet måste innehålla en mekanism för att hämta användaruppgifter. Programmet kan till exempel ge en användare ett enkelt användargränssnitt där användaren kan ange värden för användarnamn och lösenord. Dessutom bör det finnas en mekanism för hantering och begränsning av upprepade autentiseringsfel.

Skapa en händelsehanterare som skickar en uppsättning hårdkodade autentiseringsuppgifter till Primetime-objektet som händelsen härstammar från:

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

(Koden för att spela upp videon och se till att anslutningen till videoströmmen har upprättats inkluderas inte här.)
