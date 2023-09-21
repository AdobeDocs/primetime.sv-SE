---
description: Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.
title: Integrera ljud med senare bindning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Integrera ljud med senare bindning {#integrate-late-binding-audio}

Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.

* Så här skapar du en alternativ ljudhanterare:

  ```java
  AAManager aaManager = new AAManagerOn(); 
  ```

* Om du vill använda ManagerFactory för att aktivera alternativt ljud kontrollerar du att följande kodrad finns i `PlayerFragment.java` fil:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>true</b>,config, mediaPlayer);
  ```

  Så här inaktiverar du alternativt ljud:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>false</b>,config, mediaPlayer);
  ```
