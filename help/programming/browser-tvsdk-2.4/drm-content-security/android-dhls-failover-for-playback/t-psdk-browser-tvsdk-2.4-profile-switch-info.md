---
description: När mediespelaren byter sin aktuella profil till en ny profil kan du hämta information om växeln, bland annat när den växlades, information om bredd och höjd eller varför en annan bithastighet användes.
seo-description: När mediespelaren byter sin aktuella profil till en ny profil kan du hämta information om växeln, bland annat när den växlades, information om bredd och höjd eller varför en annan bithastighet användes.
seo-title: Hämta information om profilväxling
title: Hämta information om profilväxling
uuid: 0ff1aeac-882a-4209-b19f-1aa3141404d9
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Hämta information om profilväxling{#get-information-about-profile-switch}

När mediespelaren byter sin aktuella profil till en ny profil kan du hämta information om växeln, bland annat när den växlades, information om bredd och höjd eller varför en annan bithastighet användes.

1. Lyssna efter händelsen `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

   Webbläsarens TVSDK-mediespelare skickar den här händelsen när dess adaptiva bithastighetsväxlingsalgoritm växlar till en annan profil på grund av nätverks- eller datorförhållanden. (När bithastigheten eller punkten ändras.)
1. När händelsen inträffar ska du kontrollera följande egenskaper för att få information om växeln:

   * `profile`: Identifierare för den nya profilen som används.
   * `time`: Den direktuppspelningstid som växeln inträffade vid.
   * `description`: Textuell beskrivning av orsaken till en bithastighetsändring, som en sträng med semikolonavgränsade nyckel-/värdepar. Innehåller högst ett `Reason` och ett `Bitrate`. Om informationen inte är tillgänglig eller bithastigheten inte ändrades är strängen tom.

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Nyckelnamn </th> 
      <th colname="col2" class="entry"> Möjliga värden </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Orsak  </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">Nätverksanpassning </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Sök </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Profilen stöds inte </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Redundans </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Bithastighet  </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> upp  </span>: Bithastigheten ökade </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> ned  </span>: Bithastigheten minskade </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   Här är några exempel på returnerade `description`-strängar:

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`: Heltal som anger bredden i pixlar.
   * `height`: Heltal som anger höjden i pixlar.

   >[!NOTE]
   >
   >Bredd- och höjddata är bara tillgängliga när de inkluderas i taggen `RESOLUTION` i M3U8-manifestet. Om informationen inte ingår i M3U8 anges egenskaperna width och height till 0 eftersom de inte ingår i profilinformationen.
