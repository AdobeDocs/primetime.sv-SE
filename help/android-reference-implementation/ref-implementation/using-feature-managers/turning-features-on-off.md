---
description: Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.
seo-description: Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.
seo-title: Aktivera och inaktivera funktioner med ManagerFactory
title: Aktivera och inaktivera funktioner med ManagerFactory
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Aktivera och inaktivera funktioner med ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.

Argumentet enablement i exemplet nedan avgör om funktionen används eller inte. Om värdet är false skapas funktionshanteraren men bara innehåller standardfunktionaliteten för spelaren, som om funktionshanteraren inte skapades. Om det är true skapas funktionshanteraren, funktionen aktiveras och mediespelaren accepterar indata från konfigurationsfilen.

I `com.adobe.primetime.reference.ui.player.PlayerFragment.java` filen:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API-dokumentation**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)