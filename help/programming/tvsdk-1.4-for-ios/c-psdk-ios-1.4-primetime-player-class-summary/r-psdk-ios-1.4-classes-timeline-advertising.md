---
description: Dessa klasser innehåller information om annonser som förekommer i en tidslinje.
title: Tidslinjeannonsklasser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Annonsklasser för tidslinje{#timeline-advertising-classes}

Dessa klasser innehåller information om annonser som förekommer i en tidslinje.

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Namn </th> 
   <th colname="2" class="entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">En klass som definierar Ad-förkortningen och som innehåller all annonsinformation. Den definieras av ett unikt ID, en varaktighet och en MediaResource-kod. MediaResource innehåller den URL där annonsinnehållet finns. 
    <pre>
      Representerar en primär linjär resurs som delas upp i innehållet. Det kan också innehålla en array med tillhörande resurser som måste visas tillsammans med den linjära resursen.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">En klass som representerar en resurs som ska visas. 
    <pre>
      Representerar en resurs som ska visas.
    </pre> 
    <pre>
      En klass som representerar en annonsresurs.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      Visar en banderollresurs. Programmet måste skapa en ny instans av den här verktygsklassen, ange banderollresursen och lägga till den i en vy. Tryckningen och klickspårningen för banderollen hanteras internt av den här klassen.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">En klass som ger en enhetlig vy på flera annonser som kommer att spelas upp någon gång under uppspelningen. 
    <pre>
      Representerar en kontinuerlig sekvens med annonser som delas upp i innehållet.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">En klass som representerar en klickinstans som är associerad med en resurs. Den här instansen innehåller information om klicknings-URL:en och rubriken som kan användas för att ge användaren mer information. 
    <pre>
      Representerar en klickinstans som är associerad med en resurs. Den här instansen innehåller information om klicknings-URL:en och rubriken som kan användas för att ge användaren mer information.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> Protokoll som definierar egenskaper för API-anrop till AdPolicySelector. Dessa egenskaper utgör kontexten för att framtvinga varje annonsbeteende. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PTAdPolicySelector</td> 
   <td colname="2"> Ett protokoll för annonspolicyväljare för att framtvinga annonsbeteenden. Program kan följa det här protokollet genom att implementera alla nödvändiga metoder eller genom att utöka den befintliga standardprincipväljarklassen för att anpassa specifika beteenden. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> PTAdTimeline</td> 
   <td colname="2"> En klass som representerar tidslinjen för brytningar i innehållet. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> </a> PTContentResolverclass,  
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> </a> PTContentResolverprotocol
    </pre> </td> 
   <td colname="2"> En klass som hanterar annonsupplösningsdelen i Adobe Primetime annonsbeslutsprocess. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> Protokoll som beskriver de metoder som den anpassade innehållslösaren ( <span class="codeph"> PTContentResolver</span>) ska använda för att kommunicera status för innehållets matchning till delegaten. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">En klass som abstraherar en begäran om placeringsinformation. Varje löst annons måste ha en placeringsinformation kopplad till sig. Placeringsinformationen beskriver var annonsen är avsedd att placeras på tidslinjen. Den innehåller information om: 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">Placeringsposition (i ms) </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">Placeringens typ (före-, mitt- eller efterrullning) </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">Längden på det huvudinnehållssegment som ska ersättas </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

