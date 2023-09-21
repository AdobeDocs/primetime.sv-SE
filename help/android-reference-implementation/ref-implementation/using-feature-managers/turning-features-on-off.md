---
description: Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.
title: Aktivera och inaktivera funktioner med ManagerFactory
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Aktivera och inaktivera funktioner med ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.

Argumentet enablement i exemplet nedan avgör om funktionen används eller inte. Om värdet är false skapas funktionshanteraren men bara innehåller standardfunktionaliteten för spelaren, som om funktionshanteraren inte skapades. Om det är true skapas funktionshanteraren, funktionen aktiveras och mediespelaren accepterar indata från konfigurationsfilen.

I `com.adobe.primetime.reference.ui.player.PlayerFragment.java` fil:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API-dokumentation**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
