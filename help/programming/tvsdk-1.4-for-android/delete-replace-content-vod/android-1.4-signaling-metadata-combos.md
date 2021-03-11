---
description: Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.
title: Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.

>[!NOTE]
>
>När det finns en konflikt mellan tidsintervall och annonseringslägen ger TVSDK tidintervallprioritet.

**Tabell 3: Signeringsläge/Metadatakombinationsbeteenden**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Läge för annonssignalering </th> 
   <th class="entry"> Lägg till metadata </th> 
   <th class="entry"> Skapade lösare </th> 
   <th class="entry"><span class="codeph"> </span> PlacementInformationskapad </th> 
   <th class="entry"> Resulterande beteende </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>Serveröversikt</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> Ta bort </td> 
   <td> Ta bort </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Raderade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervall borttagna, annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ersätt, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervall som ersatts </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall, inga annonser infogade </td> 
  </tr> 
  <tr> 
   <td> <b>Manifest Cues</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> Annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervall borttagna, annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall, inga annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort </td> 
   <td> Ta bort </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Raderade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ersätt, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervall som ersatts </td> 
  </tr> 
  <tr> 
   <td> <b>Anpassat tidsintervall</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort </td> 
   <td> Ta bort </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Raderade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervall borttagna, inga annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> Ingen </td> 
   <td> Inga annonser har infogats </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ersätt, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervall ersatta med annonser </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Anpassad annons, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall, inga annonser infogade </td> 
  </tr> 
  <tr> 
   <td> <b>Inte inställd (standard)</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort </td> 
   <td> Ta bort </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Raderade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ta bort, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Intervall borttagna, annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Annonser infogade </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Ersätt, Auditude </td> 
   <td> Ta bort, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervall ersatta med annonser </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Markerade intervall </td> 
  </tr> 
 </tbody> 
</table>

