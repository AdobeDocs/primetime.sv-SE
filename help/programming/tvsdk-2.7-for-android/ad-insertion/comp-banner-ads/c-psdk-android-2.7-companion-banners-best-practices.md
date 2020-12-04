---
description: 'null'
seo-description: 'null'
seo-title: Bästa tillvägagångssätt för annonser på följeslagare
title: Bästa tillvägagångssätt för annonser på följeslagare
uuid: d844babb-20ab-4380-9487-eb1c24b58877
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Banderollannonser {#companion-banner-ads}

TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.

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

