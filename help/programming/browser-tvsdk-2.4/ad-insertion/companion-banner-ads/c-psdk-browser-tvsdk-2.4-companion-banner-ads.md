---
description: Webbläsaren TVSDK har stöd för banners, som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.
title: Companion banner ads
exl-id: 73b5c9b0-abac-47ed-a21d-3f8f90cc5b55
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Översikt {#companion-banner-ads-overview}

Webbläsaren TVSDK har stöd för banners, som är annonser som medföljer en linjär annons och ofta finns kvar på sidan när den linjära annonsen är slut. Ditt program ansvarar för att visa de övriga banderoller som levereras med en linjär annons.

Följ dessa rekommendationer när du visar följeslagarannonser:

* Försök att presentera så många banners som passar in i spelarens layout.
* Visa bara en tilläggsbanderoll om du har en plats som matchar den angivna höjden och bredden på den tillhörande banderollen.

   >[!TIP]
   >
   >Ändra inte storlek på banderollen.

* Presentera den eller de tillhörande banderollerna så snart som möjligt efter det att annonsen börjar.
* Täck inte över huvud-annons-/videobehållaren med pekbanderoller.
* Fortsätt visa tilläggsbanners när annonsen är slut.

   Standarden är att visa varje pekbanderoll tills du har en ersättare för den här banderollen.
