---
title: Bästa tillvägagångssätt för annonser på följeslagare
description: Bästa tillvägagångssätt för annonser på följeslagare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Banderollannonser {#companion-banner-ads}

TVSDK har stöd för bannerannonser som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.

## Bästa tillvägagångssätt för annonser på följeslagare {#best-practices-for-companion-banner-ads}

Följ de här rekommendationerna när du visar följeslagarannonser:

* Försök att presentera så många banners som passar in i spelarens layout.
* Visa bara en tilläggsbanderoll om du har en plats som matchar annonsens angivna höjd och bredd.

  >[!IMPORTANT]
  >
  >Ändra inte storlek på annonsen.

* Börja presentera banderollerna så snart som möjligt efter att annonsen har startats.
* Täck inte över huvud-annons-/videobehållaren med pekbanderoller.
* Du kan visa tilläggsbanderoller när annonsen är slut.

  Standardmetoden är att visa varje pekbanderoll tills du har en ersättare för annonsen.
