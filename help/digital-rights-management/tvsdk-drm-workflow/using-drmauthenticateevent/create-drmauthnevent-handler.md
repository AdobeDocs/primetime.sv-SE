---
description: DRMAuthenticateEvent-objektet skickas när ett Primetime-objekt försöker att spela upp skyddat innehåll som kräver inloggningsuppgifter för autentisering innan uppspelning (och autentisering ännu inte har utförts). DRMAuthenticateEvent-hanteraren samlar in de inloggningsuppgifter som krävs (användarnamn, lösenord och typ) och skickar värdena till .setDRMAuthenticationCredentials()-metoden för validering.
seo-description: DRMAuthenticateEvent-objektet skickas när ett Primetime-objekt försöker att spela upp skyddat innehåll som kräver inloggningsuppgifter för autentisering innan uppspelning (och autentisering ännu inte har utförts). DRMAuthenticateEvent-hanteraren samlar in de inloggningsuppgifter som krävs (användarnamn, lösenord och typ) och skickar värdena till .setDRMAuthenticationCredentials()-metoden för validering.
seo-title: Skapa en DRMAuthenticateEvent-hanterare
title: Skapa en DRMAuthenticateEvent-hanterare
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

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
