---
description: TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.
seo-description: TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.
seo-title: Companion banner ads
title: Companion banner ads
uuid: 6f38f6ec-bc8b-4ea1-845f-90031b3d8a00
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Companion banner ads {#companion-banner-ads}

TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.

Följ dessa rekommendationer när du visar följeslagarannonser:

* Försök att presentera så många banners som passar in i spelarens layout.
* Visa bara en tilläggsbanderoll om du har en plats som exakt matchar den angivna höjden och bredden.

   >[!TIP]
   >
   >Ändra inte storlek på banderollen.

* Presentera den eller de tillhörande banderollerna så snart som möjligt efter det att annonsen börjar.
* Täck inte över huvud-annons-/videobehållaren med pekbanderoller.
* Fortsätt visa tilläggsbanners när annonsen är slut.

   Standarden är att visa varje pekbanderoll tills du har en ersättare för den här banderollen.

## Kompletterande banderolldata {#companion-banner-data}

Innehållet i en PTAdAsset beskriver en tilläggsbanderoll.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Meddelandet returnerar `PTMediaPlayerAdStartedNotification` en `PTAd` instans som innehåller en `companionAssets` egenskap (array med `PtAdAsset`).
Var och en `PtAdAsset` innehåller information om hur resursen visas.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tillgänglig information </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Bredden på den tillhörande banderollen i pixlar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Den kompletterande banderollens höjd i pixlar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> resurstyp </td> 
   <td colname="col2">Resurstypen för den här tilläggsbanderollen: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Data finns i HTML-kod. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Data är en iframe-URL (src). </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">statisk: Data är en staticURL som är en direkt URL till en bild. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> data </td> 
   <td colname="col2"> Data av den typ som anges av <span class="codeph"> resourceType</span> för den här tilläggsbanderollen. </td> 
  </tr> 
 </tbody> 
</table>

## Visa banners {#display-banner-ads}

Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.

TVSDK tillhandahåller en lista över bannerannonser som är kopplade till en linjär annons via `PTMediaPlayerAdPlayStartedNotification` meddelandehändelsen.

Manifester kan ange banners för följeslagare genom att:

* Ett HTML-fragment
* URL:en för en iFrame-sida
* URL:en för en statisk bild eller en Adobe Flash SWF-fil

För varje kompletterande annons visar TVSDK vilka typer som är tillgängliga för ditt program.

1. Skapa en `PTAdBannerView` instans för varje extern annonsplats på sidan.

       Kontrollera att följande information har lämnats:
   
   * För att förhindra att följesedlar av olika storlek hämtas, en banderollinstans som anger bredd och höjd.
   * Standardstorlekar för banderoller.

1. Lägg till en observatör för `PTMediaPlayerAdStartedNotification` som gör följande:
   1. Rensar befintliga annonser i banderollinstansen.
   1. Hämtar listan över följeslagarannonser från `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Om listan med följesedlar inte är tom kan du iterera över listan för banderollinstanser.

      Varje bannerinstans ( a `PTAdAsset`) innehåller information som bredd, höjd, resurstyp (html, iframe eller static) och data som krävs för att visa den tillhörande banderollen.
   1. Om en videoannons inte har några följeslagare bokade med sig innehåller listan med följesedlar inga data för den videoannonsen.

      Om du vill visa en fristående visningsannons lägger du till logiken i skriptet för att köra en vanlig DFP-visningstagg (DoubleClick for Publishers) i rätt banderollinstans.
   1. Skickar banderollinformationen till en funktion på sidan som visar banderollerna på lämplig plats.

      Detta är vanligtvis en `div`stil, och funktionen använder `div ID` för att visa banderollen. Exempel:

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
