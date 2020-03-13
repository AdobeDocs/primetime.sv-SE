---
description: Skapa Video Analytics Manager
seo-description: Skapa Video Analytics Manager
seo-title: Skapa Video Analytics Manager
title: Skapa Video Analytics Manager
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Skapa Video Analytics Manager {#create-the-video-analytics-manager}

En ny hanterarklass ( `VAManager`) har lagts till i referensimplementeringen av Android. `VAManager` skapar och förstör helt enkelt en instans av `VideoHeartbeat` klassen. Referensimplementeringen skapar en `VAManager` instans när en ny `MediaPlayer` skapas och förstör den instansen när den `MediaPlayer` förstörs. Detta implementeras i `PlayerFragment.java`.

## Skapa en ny videoanalyshanterare

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

Variabeln config är en konkret implementering av `IVAConfig` och innehåller `VideoHeartbeat` körningskonfigurationerna.

>[!NOTE]
>
>Om Android-programmet inte har konfigurerats med ett Adobe Analytics-konto genereras inga data för videospårning, även om en instans av `VAManager` skapas och aktiveras.

