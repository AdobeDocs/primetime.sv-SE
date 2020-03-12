---
description: 'null'
seo-description: 'null'
seo-title: Bästa tillvägagångssätt för annonser på följeslagare
title: Bästa tillvägagångssätt för annonser på följeslagare
uuid: 0e4c98cd-5e16-4c84-848f-02bc6f1b0d6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Bästa tillvägagångssätt för annonser på följeslagare {#best-practices-for-companion-banner-ads}

TVSDK har stöd för banners som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.

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