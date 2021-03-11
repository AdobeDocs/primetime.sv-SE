---
description: Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.
title: Aktivera och inaktivera funktioner med ManagerFactory
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Aktivera och inaktivera funktioner med ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.

Argumentet enablement i exemplet nedan avgör om funktionen används eller inte. Om värdet är false skapas funktionshanteraren men bara innehåller standardfunktionaliteten för spelaren, som om funktionshanteraren inte skapades. Om det är true skapas funktionshanteraren, funktionen aktiveras och mediespelaren accepterar indata från konfigurationsfilen.

I filen `com.adobe.primetime.reference.ui.player.PlayerFragment.java`:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API-dokumentation**:  [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)