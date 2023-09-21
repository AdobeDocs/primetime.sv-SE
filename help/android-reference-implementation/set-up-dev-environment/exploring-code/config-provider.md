---
description: Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.
title: ConfigProvider
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.

Du använder [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) klassen som ska implementera `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`och `IQosConfig` konfigurationsgränssnitt så att funktionshanterarna kan läsa konfigurationerna. Till exempel `ICCConfig` är gränssnittet för `CCManager` konfiguration. Konfigurationsfilerna tar emot konfigurationsparametrarna från JSON-konfigurationsfilen.

The `ConfigProvider.java` -filen är ett exempel på Adobe implementering av konfigurationsgränssnitten. Inställningarna läses från `SharedPreferences`, där konfigurationen lagras. Du kan spara konfigurationen på alla sätt som fungerar för din organisation. Konfigurationsimplementeringen tillhandahåller en wrapper för konfigurationskällan.
