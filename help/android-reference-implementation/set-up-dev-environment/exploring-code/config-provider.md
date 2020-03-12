---
description: Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.
seo-description: Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# ConfigProvider {#configprovider}

Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.

Du använder [klassen ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) för att implementera gränssnitten `ICCConfig`, `IAAConfig`, `IPlaybackConfig`och `IAdConfig``IQosConfig` så att funktionshanterarna kan läsa konfigurationerna. Detta `ICCConfig` är till exempel gränssnittet för `CCManager` konfigurationen. Konfigurationsfilerna tar emot konfigurationsparametrarna från JSON-konfigurationsfilen.

Filen `ConfigProvider.java` är ett exempel på Adobes implementering av konfigurationsgränssnitten. Den läser inställningarna från `SharedPreferences`den plats där konfigurationen lagras. Du kan spara konfigurationen på alla sätt som fungerar för din organisation. Konfigurationsimplementeringen tillhandahåller en wrapper för konfigurationskällan.