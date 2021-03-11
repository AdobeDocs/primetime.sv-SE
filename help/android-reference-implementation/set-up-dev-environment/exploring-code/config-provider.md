---
description: Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.
title: ConfigProvider
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.

Du använder klassen [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) för att implementera konfigurationsgränssnitten `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` och `IQosConfig` så att funktionshanterarna kan läsa konfigurationerna. `ICCConfig` är till exempel gränssnittet för konfigurationen `CCManager`. Konfigurationsfilerna tar emot konfigurationsparametrarna från JSON-konfigurationsfilen.

Filen `ConfigProvider.java` är ett exempel på Adobe-implementering av konfigurationsgränssnitten. Den läser inställningarna från `SharedPreferences`, där konfigurationen lagras. Du kan spara konfigurationen på alla sätt som fungerar för din organisation. Konfigurationsimplementeringen tillhandahåller en wrapper för konfigurationskällan.