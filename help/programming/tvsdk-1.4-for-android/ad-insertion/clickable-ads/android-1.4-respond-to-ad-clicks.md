---
description: När en användare klickar på en annons eller en relaterad knapp måste programmet svara. TVSDK ger dig information om mål-URL:en för klickningen.
seo-description: När en användare klickar på en annons eller en relaterad knapp måste programmet svara. TVSDK ger dig information om mål-URL:en för klickningen.
seo-title: Svara på klickningar på annonser
title: Svara på klickningar på annonser
uuid: 31852f01-c900-48e3-ae23-7fb131c22594
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Svara på klickningar på annonser{#respond-to-clicks-on-ads}

När en användare klickar på en annons eller en relaterad knapp måste programmet svara. TVSDK ger dig information om mål-URL:en för klickningen.

1. Om du vill konfigurera en händelseavlyssnare för TVSDK och ange klickningsinformationen registrerar du en `AdClickedEventListener.onAdClicked`.

   När en användare klickar på en annons eller en relaterad knapp skickar TVSDK det här meddelandet, inklusive information om klickningens mål.
1. Övervaka användarinteraktioner i klickbara annonser.
1. När användaren rör vid eller klickar på annonsen eller knappen kan du kontakta TV SDK `notifyClick` på `MediaPlayerView`.
1. Lyssna efter `onAdClick(AdClickEvent event)` eventet från TVSDK.
1. Om du vill hämta klicknings-URL:en och relaterad information använder du metoderna för `AdClickEvent` instansen.
1. Pausa videon.

   Mer information om hur du pausar videon finns i [Pausa och återuppta uppspelning.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Använd klickningsinformationen för att visa webbadressen för annonsklickningen och relaterad information.

       Du kan till exempel visa informationen på något av följande sätt:
   
   * Öppna klicknings-URL:en i en webbläsare i programmet.

      På skrivbordsplattformar används video- och uppspelningsområdet för att anropa klicknings-URL:er när användaren klickar.
   * Omdirigera användare till deras externa webbläsare för mobila enheter.

      På mobila enheter används video- och uppspelningsområdet för andra funktioner, som att dölja och visa kontroller, pausa uppspelning, expandera till helskärm och så vidare. På dessa enheter används en separat vy, till exempel en sponsorknapp, för att starta klicknings-URL:en.

1. Stäng webbläsarfönstret där genomklickningsinformationen visas och återuppta uppspelningen av videon.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

Exempel:

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
 
    } 
}; 
```

