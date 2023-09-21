---
description: Skapa Video Analytics Manager
title: Skapa Video Analytics Manager
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Skapa Video Analytics Manager {#create-the-video-analytics-manager}

En ny hanterarklass ( `VAManager`) har lagts till i Android-referensimplementeringen. `VAManager` skapar och förstör helt enkelt en instans av `VideoHeartbeat` klassen. Referensimplementeringen skapar en `VAManager` instans när en ny `MediaPlayer` skapas och tas bort när `MediaPlayer` förstörs. Detta implementeras i `PlayerFragment.java`.

## Skapa en ny videoanalyshanterare

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

Konfigurationsvariabeln är en konkret implementering av `IVAConfig` och innehåller körningsmiljön `VideoHeartbeat` konfigurationer.

>[!NOTE]
>
>Om Android-programmet inte har konfigurerats med ett Adobe Analytics-konto genereras inga data för videospårning, även om en instans av `VAManager` skapas och aktiveras.
