---
description: PTNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
seo-description: PTNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.
seo-title: Meddelanden om spelarstatus, aktivitet, fel och loggar
title: Meddelanden om spelarstatus, aktivitet, fel och loggar
uuid: 59716a66-3736-4076-8011-8104bfe3a83a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Meddelanden om spelarstatus, aktivitet, fel och loggning {#notifications-for-player-status-activity-errors-and-logs-overview}

PTNotification-objekt innehåller information om ändringar i spelarstatus, varningar och fel. Fel som stoppar videouppspelningen orsakar också en statusändring för spelaren.

Programmet kan hämta information om meddelanden och status. Du kan också skapa ett loggningssystem för diagnostik och validering genom att använda meddelandeinformationen.

>[!IMPORTANT]
>
>TVSDK använder också *`notification`* för att referera till `NSNotifications` meddelanden ( `PTMediaPlayer` meddelanden) *`event`* som skickas för att ge information om spelaraktivitet.

TVSDK utfärdar även problem `PTMediaPlayerNewNotificationItemEntryNotification` när det utfärdar `PTNotification`.

Du implementerar händelseavlyssnare för att hämta och svara på händelser. Många händelser ger `PTNotification` statusmeddelanden.

## Meddelandeinnehåll {#notification-content}

PTNotification ger information som är relaterad till spelarens status.

TVSDK tillhandahåller en kronologisk lista över `PTNotification` meddelanden. Varje anmälan innehåller följande information:

* Tidsstämpel
* Diagnostiska metadata som består av följande element:

   * `type`: INFORMATION, VARNING eller FEL.
   * `code`: En numerisk representation av anmälan.
   * `name`: En beskrivning av meddelandet som kan läsas av människor, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` ger till exempel ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till ett annat `PTNotification` objekt som direkt påverkar det här meddelandet.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.

## Meddelandeinställning {#notification-setup}

TVSDK konfigurerar spelaren för grundläggande meddelanden, men du måste slutföra samma inställning för dina anpassade meddelanden.

Det finns två implementeringar för `PTNotification`:

* Att lyssna
* Lägga till anpassade meddelanden i `PTNotificationHistory`

Om du vill lyssna på meddelanden instansierar TVSDK `PTNotification` klassen och bifogar den till en instans av `PTMediaPlayerItem`som är kopplad till en PTMediaPlayer-instans. Det finns bara en `PTNotificationHistory` instans per `PTMediaPlayer`.

>[!IMPORTANT]
>
>Om du lägger till anpassningar måste dina program, och inte TVSDK, utföra dessa steg.

## Lyssna på meddelanden {#listen-to-notifications}

Det finns två sätt att lyssna på `PTNotification` meddelandet i `PTMediaPlayer`:

1. Kontrollera manuellt `PTNotificationHistory` om `PTMediaPlayerItem` det finns en timer och kontrollera skillnaderna:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Använd den publicerade [NSN-aviseringen](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) för `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registrera dig på `NSNotification` genom att använda instansen av `PTMediaPlayer` varifrån du vill få meddelanden:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementera återanrop för meddelanden {#implement-notification-callbacks}

Du kan implementera återanrop för meddelanden.

1. Implementera callback-funktionen för meddelanden genom att hämta informationen `PTNotification` från `NSNotification` användarinformationen och läsa dess värden med hjälp av `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Lägg till anpassade meddelanden {#add-custom-notifications}

Så här lägger du till ett anpassat meddelande:
Skapa ett nytt `PTNotification` och lägg till det i `PTNotificationHistory` genom att använda det aktuella `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
