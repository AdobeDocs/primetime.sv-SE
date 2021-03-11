---
description: Skapa Video Analytics Manager
title: Skapa Video Analytics Manager
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Skapa videoanalyshanteraren {#create-the-video-analytics-manager}

En ny hanterarklass ( `VAManager`) har lagts till i referensimplementeringen för Android. `VAManager` skapar och förstör helt enkelt en instans av  `VideoHeartbeat` klassen. Referensimplementeringen skapar en `VAManager`-instans när en ny `MediaPlayer` skapas och förstör den instansen när `MediaPlayer` förstörs. Detta implementeras i `PlayerFragment.java`.

## Skapa en ny videoanalyshanterare

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

Konfigurationsvariabeln är en konkret implementering av `IVAConfig` och innehåller `VideoHeartbeat`-konfigurationer för körningen.

>[!NOTE]
>
>Om Android-programmet inte har konfigurerats med ett Adobe Analytics-konto genereras inga data för videospårning, även om en instans av `VAManager` skapas och aktiveras.

