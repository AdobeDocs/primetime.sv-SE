---
description: Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.
title: Integrera ljud med senare bindning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Integrera det senast bindande ljudet {#integrate-late-binding-audio}

Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.

* Så här skapar du en alternativ ljudhanterare:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Om du vill använda ManagerFactory för att aktivera alternativt ljud kontrollerar du att följande kodrad finns i `PlayerFragment.java`-filen:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Så här inaktiverar du alternativt ljud:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

