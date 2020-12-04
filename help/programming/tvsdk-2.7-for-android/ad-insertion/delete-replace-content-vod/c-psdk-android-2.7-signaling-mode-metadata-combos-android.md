---
description: Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.
seo-description: Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.
seo-title: Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer
title: Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer
uuid: 7b2a5588-110d-4ce5-aa9c-706d357f211d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.

>[!TIP]
>
>När det finns en konflikt mellan tidsintervall och annonseringslägen ger TVSDK tidintervallprioritet.

Följande tabell innehåller information om signaleringsläget och metadatakombinationsbeteenden:

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
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
   <td colname="1"> <p><b>Serveröversikt</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Manifest Cues</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
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
   <td colname="1"> <p><b>Anpassat tidsintervall</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td colname="1"> <p><b>Inte inställd (standard)</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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

