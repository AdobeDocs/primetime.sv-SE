---
description: TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.
title: Companion banner ads
exl-id: c10a38ec-acbb-4e84-aff2-c93c9b1cec81
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

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

Innehållet i en AdBannerAsset beskriver en tilläggsbanderoll.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

The `AdPlaybackEvent.AD_STARTED` returnerar en `Ad` instans som innehåller en `companionAssets` egenskap ( `Vector.<AdAsset>`).
Varje `AdAsset` innehåller information om hur resursen visas.

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
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> banderolldata </td> 
   <td colname="col2"> Data av den typ som anges av <span class="codeph"> resourceType</span> för den här följeslagaren. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> statisk URL </td> 
   <td colname="col2"> <p>Ibland har den tillhörande banderollen också en staticURL som är en direkt URL till bilden eller en <span class="filepath"> .swf</span> (flash banner). </p> <p>Om du inte vill använda html eller iframe kan du använda en direkt URL till en bild eller swf för att visa banderollen på scenen Flash i stället. I det här fallet kan du använda staticURL för att visa banderollen. </p> <p>Viktigt: Du måste kontrollera om den statiska URL:en är en giltig sträng, eftersom den här egenskapen kanske inte alltid är tillgänglig. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Visa banners {#display-banner-ads}

Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta TVSDK att lyssna efter annonsrelaterade händelser.

TVSDK tillhandahåller en lista över bannerannonser som är kopplade till en linjär annons via `AdPlaybackEvent.AD_STARTED` event.

Manifester kan ange banners för följeslagare genom att:

* Ett HTML-fragment
* URL:en för en iFrame-sida
* URL-adressen till en statisk bild eller en Adobe Flash SWF-fil

För varje kompletterande annons visar TVSDK vilka typer som är tillgängliga för ditt program.

Lägg till en avlyssnare för `AdPlaybackEvent.AD_STARTED` händelse som gör följande:

1. Rensar befintliga annonser i banderollinstansen.

1. Hämtar listan över annonser från `Ad.companionAssets`.

1. Om listan med följesedlar inte är tom kan du iterera över listan för banderollinstanser.

   Varje banner-instans ( `AdBannerAsset`) innehåller information som bredd, höjd, resurstyp (html, iframe eller static) och data som krävs för att visa den tillhörande banderollen.

1. Om en videoannons inte har några följeslagare bokade med sig innehåller listan med följesedlar inga data för den videoannonsen.

   Om du vill visa en fristående visningsannons lägger du till logiken i skriptet för att köra en vanlig DFP-visningstagg (DoubleClick for Publishers) i rätt banderollinstans.

1. Skickar banderollinformationen till en funktion på sidan, vanligen JavaScript, med `ExternalInterface`, som visar banners på lämplig plats.

   Detta är vanligtvis en `div`och funktionen använder `div ID` för att visa banderollen. Till exempel:

   Lägg till händelseavlyssnaren:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementera avlyssnarhanteraren:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
           for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
               } 
           } 
       }  
       //...        
   }
   ```

   Exempel på JavaScript som ska hantera visningen:

   ```js
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
