---
description: Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.
title: Konfigurera adaptiva bithastigheter med ABRControlParameters
exl-id: 53ca8516-b449-46c8-baa9-9d0d5800b3c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Konfigurera adaptiva bithastigheter med ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.

Följande villkor gäller för `ABRControlParameters`:

* Du måste ange värden för alla parametrar under konstruktionstiden.
* Du kan inte ändra enskilda värden efter byggtiden.
* Om parametrarna som du anger ligger utanför det tillåtna intervallet kan du `ArgumentError` kastas.

1. Bestäm ABR-principen:

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. Ange ABR-parametervärden i dialogrutan `ABRControlParameters` och tilldela dem till Media Player.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
