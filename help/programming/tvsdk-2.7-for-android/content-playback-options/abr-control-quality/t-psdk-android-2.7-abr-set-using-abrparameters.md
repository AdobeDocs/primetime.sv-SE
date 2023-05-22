---
description: Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.
title: Konfigurera adaptiva bithastigheter med ABRControlParameters
exl-id: fc7887bd-37e8-48e7-8afb-3946fb3f1e77
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Konfigurera adaptiva bithastigheter med ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.

Följande villkor gäller för `ABRControlParameters`:

* Vid konstruktionen måste du ange värden för alla parametrar.
* Efter konstruktionen kan du inte ändra enskilda värden.
* Om parametrarna som du anger ligger utanför det tillåtna intervallet kan du `ArgumentError` kastas.

1. Bestäm den inledande, lägsta och högsta bithastigheten.
1. Bestäm ABR-principen:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Ange ABR-parametervärden i dialogrutan `ABRControlParameters` och tilldela värdena till Media Player.

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
