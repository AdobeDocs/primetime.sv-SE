---
description: Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.
seo-description: Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.
seo-title: Konfigurera adaptiva bithastigheter med ABRControlParameters
title: Konfigurera adaptiva bithastigheter med ABRControlParameters
uuid: c877c5cc-ad72-46dc-afc4-d41ee097a9a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Konfigurera adaptiva bithastigheter med ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Du kan bara ange ABR-kontrollvärden med ABRControlParameters, men du kan när som helst skapa en ny.

Följande villkor gäller `ABRControlParameters`:

* Du måste ange värden för alla parametrar under konstruktionstiden.
* Du kan inte ändra enskilda värden efter byggtiden.
* Om parametrarna som du anger ligger utanför det tillåtna intervallet `ArgumentError` genereras ett fel.

1. Bestäm den inledande, lägsta och högsta bithastigheten.
1. Bestäm ABR-principen:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Ange ABR-parametervärden i konstruktorn och tilldela dem till Media Player. `ABRControlParameters`

   ```java
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```

