---
description: Du kan implementera ett eget loggningssystem.
title: Anpassad loggning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Anpassad loggning {#customized-logging}

Du kan implementera ett eget loggningssystem.

Förutom att logga med hjälp av fördefinierade meddelanden kan du implementera ett loggningssystem som använder dina loggmeddelanden och meddelanden som genereras av TVSDK. Mer information om fördefinierade meddelanden finns i [Meddelandesystemet](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). Du kan använda dessa loggar för att felsöka dina spelarprogram och för att få en bättre förståelse för arbetsflödet för uppspelning och annonsering.

Anpassad loggning använder en delad singleton-instans av `PSDKPTLogFactory`, som har en funktion för att logga meddelanden till flera loggare. Du definierar och lägger till (registrerar) en eller flera loggare i `PTLogFactory`. På så sätt kan du definiera flera loggare med anpassade implementeringar, som en konsollogg, en webblogg eller en konsolhistoriklogg.

TVSDK genererar loggmeddelanden för många av sina aktiviteter, som `PTLogFactory` vidarebefordra till alla registrerade loggare. Programmet kan också generera anpassade loggmeddelanden som vidarebefordras till alla registrerade loggare. Varje loggare kan filtrera meddelandena och vidta lämpliga åtgärder.

Det finns två implementeringar för `PTLogFactory`:

* För avlyssning av loggar.
* Lägga till loggar i en `PTLogFactory`.

## Lyssna på loggar {#listen-to-logs}

Så här registrerar du dig för avlyssning av loggar:
1. Implementera en anpassad klass som följer protokollet `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. Om du vill registrera instansen för att ta emot loggningsposter lägger du till en instans av `PTLogger` till `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Här är ett exempel på hur du filtrerar loggar med `PTLogEntry` typ:

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## Lägg till nya loggmeddelanden {#add-new-log-messages}

Så här registrerar du dig för att lyssna på loggar:
1. Skapa ett nytt `PTLogEntry` och lägg till `thePTLogFactory`:

   Du kan instansiera en `PTLogEntry` och lägg till det i `PTLogFactory` delade instanser eller använd något av makrona för att utföra samma uppgift.

   Här är ett exempel på hur du loggar med `PTLogDebug` makro:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
