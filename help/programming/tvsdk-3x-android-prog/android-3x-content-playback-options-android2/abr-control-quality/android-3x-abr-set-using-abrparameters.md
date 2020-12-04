---
description: Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.
seo-description: Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.
seo-title: Konfigurera adaptiva bithastigheter med ABRControlParameters
title: Konfigurera adaptiva bithastigheter med ABRControlParameters
uuid: 283ccd3d-535b-43ca-8ca5-82d12df31798
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Konfigurera adaptiva bithastigheter med ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.

Följande villkor gäller för `ABRControlParameters`:

* Vid konstruktionen måste du ange värden för alla parametrar.
* Efter konstruktionen kan du inte ändra enskilda värden.
* Om parametrarna som du anger ligger utanför det tillåtna intervallet genereras ett `ArgumentError`.

1. Bestäm den inledande, lägsta och högsta bithastigheten.
1. Bestäm ABR-principen:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Ange ABR-parametervärden i konstruktorn `ABRControlParameters` och tilldela värdena till Media Player.

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
