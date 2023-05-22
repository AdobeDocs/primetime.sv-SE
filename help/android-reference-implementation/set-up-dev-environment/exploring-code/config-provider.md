---
description: Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

Klassen ConfigProvider hämtar konfigurationen för mediespelaren. Du måste implementera konfigurationsgränssnittet så att funktionshanterarna kan läsa konfigurationsinformationen.

Du använder [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) klassen som ska implementera `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`och `IQosConfig` konfigurationsgränssnitt så att funktionshanterarna kan läsa konfigurationerna. Till exempel `ICCConfig` är gränssnittet för `CCManager` konfiguration. Konfigurationsfilerna tar emot konfigurationsparametrarna från JSON-konfigurationsfilen.

The `ConfigProvider.java` -filen är ett exempel på Adobe implementering av konfigurationsgränssnitten. Inställningarna läses från `SharedPreferences`, där konfigurationen lagras. Du kan spara konfigurationen på alla sätt som fungerar för din organisation. Konfigurationsimplementeringen tillhandahåller en wrapper för konfigurationskällan.
