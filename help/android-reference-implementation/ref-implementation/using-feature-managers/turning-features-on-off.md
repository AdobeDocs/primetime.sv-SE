---
description: Du kan aktivera och inaktivera funktioner utan att gå igenom koden med hjälp av hanterarfabriken.
title: Aktivera och inaktivera funktioner med ManagerFactory
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
