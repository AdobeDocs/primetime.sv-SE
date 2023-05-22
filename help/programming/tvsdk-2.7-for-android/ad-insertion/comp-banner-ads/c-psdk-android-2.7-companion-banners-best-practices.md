---
title: Bästa tillvägagångssätt för annonser på följeslagare
description: Bästa tillvägagångssätt för annonser på följeslagare
copied-description: true
exl-id: 9a335dfc-3de2-45bf-b17e-0330a5d50606
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Companion banner ads {#companion-banner-ads}

TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.

## Bästa tillvägagångssätt för annonser på följeslagare {#best-practices-for-companion-banner-ads}

Följ dessa rekommendationer när du visar följeslagarannonser:

* Försök att presentera så många banners som passar in i spelarens layout.
* Visa bara en tilläggsbanderoll om du har en plats som matchar annonsens angivna höjd och bredd.

   >[!IMPORTANT]
   >
   >Ändra inte storlek på annonsen.

* Börja presentera banderollerna så snart som möjligt efter att annonsen har startats.
* Täck inte över huvud-annons-/videobehållaren med pekbanderoller.
* Du kan visa tilläggsbanderoller när annonsen är slut.

   Standardmetoden är att visa varje pekbanderoll tills du har en ersättare för annonsen.
