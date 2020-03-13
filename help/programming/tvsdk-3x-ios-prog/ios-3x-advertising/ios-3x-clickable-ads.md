---
description: TVSDK ger dig information så att du kan agera på klickbara annonser. När du skapar användargränssnittet måste du bestämma hur du ska svara när en användare klickar på en klickbar annons.
seo-description: TVSDK ger dig information så att du kan agera på klickbara annonser. När du skapar användargränssnittet måste du bestämma hur du ska svara när en användare klickar på en klickbar annons.
seo-title: Klickbara annonser
title: Klickbara annonser
uuid: 8b257483-8b90-47cf-be2a-095b6d5b8883
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Klickbara annonser {#clickable-ads}

TVSDK ger dig information så att du kan agera på klickbara annonser. När du skapar användargränssnittet måste du bestämma hur du ska svara när en användare klickar på en klickbar annons.

I TVSDK för iOS går det bara att klicka på linjära annonser.

## Svara på klickningar på annonser {#section_537AF2593FDB4257B81AAE2103B0C719}

När en användare klickar på en annons, en tilläggsbanderoll eller en relaterad knapp måste ditt program svara. TVSDK ger dig information om mål-URL:en för klickningen.

1. Om du vill konfigurera en händelseavlyssnare för TVSDK och ange klickningsinformationen lägger du till en observatör för `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >När en användare klickar på en annons, en tilläggsbanderollannons eller en relaterad knapp skickar TVSDK det här meddelandet, inklusive information om klickningens mål.

1. Övervaka användarinteraktioner i klickbara annonser.
1. När användaren vidrör eller klickar på annonsen eller knappen ska du använda för att meddela TVSDK `[_player notifyClick:_currentAd.primaryAsset];`.
1. Lyssna efter `PTMediaPlayerAdClickNotification` eventet från TVSDK.
1. Använd `PTMediaPlayerAdClickURLKey` objektet om du vill hämta klicknings-URL:en och relaterad information.
1. Pausa videon.
1. Använd klickningsinformationen för att visa webbadressen för annonsklickningen och relaterad information.

   >[!NOTE]
   >
   >Du kan till exempel visa informationen på något av följande sätt:

   * Öppna klicknings-URL:en i en webbläsare i programmet.

      På skrivbordsplattformar används video- och uppspelningsområdet för att anropa klicknings-URL:er när användaren klickar.
   * Omdirigera användare till deras externa webbläsare för mobila enheter.

      På mobila enheter används video- och uppspelningsområdet för andra funktioner, som att dölja och visa kontroller, pausa uppspelning, expandera till helskärm och så vidare. På dessa enheter används en separat vy, till exempel en sponsorknapp, för att starta klicknings-URL:en.

1. Stäng webbläsarfönstret där genomklickningsinformationen visas och återuppta uppspelningen av videon.

   Exempel:

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```
