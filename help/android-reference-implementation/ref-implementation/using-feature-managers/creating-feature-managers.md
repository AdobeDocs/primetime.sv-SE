---
description: TVSDK-funktioner drivs av konfiguration och implementeras via MediaPlayer.
title: Skapa funktionshanterare genom att skicka konfigurationsinformation till MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Skapa funktionshanterare genom att skicka konfigurationsinformation till MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

TVSDK-funktioner drivs av konfiguration och implementeras via MediaPlayer.

* Konfiguration är en lista med specifika inställningar för funktionen, till exempel inledande bithastighet för ABR-kontroll och synlighet för stängd bildtext som standard.

   Funktionshanterare måste hämta konfigurationerna för att kunna avgöra funktionens beteende.

   I referensimplementeringen av Primetime lagras konfigurationen i delade inställningar, men du kan lagra konfigurationen på det sätt som passar din miljö bäst.

* `MediaPlayer` är det TVSDK-mediespelarobjekt som innehåller videoresursen.

   Funktionshanterare registrerar TVSDK-händelseavlyssnare för det här spelarobjektet, hämtar data från uppspelningssessionen och utlöser TVSDK-funktioner till uppspelningssessionen.

Varje funktion har ett motsvarande konfigurationsgränssnitt. `CCManager` använder till exempel `ICCConfig` för att hämta konfigurationen. `ICCConfig` innehåller metoder för att hämta konfigurationsinformation som endast gäller undertextning.

I följande exempel visas filen [!DNL ICCConfig.java] som är konfigurerad att ta emot information om synlighet för undertexter, teckensnittsstil och teckensnittskant från `MediaPlayer`:

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

Ett program som använder en TVSDK-funktion kan skapa sin funktionshanterare med en konfigurationsprovider och ett `MediaPlayer`-objekt. Exempel:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

API-dokument för funktionshanterarens konfiguration: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)