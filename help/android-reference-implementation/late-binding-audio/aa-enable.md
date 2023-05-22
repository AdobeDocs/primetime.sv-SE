---
description: Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.
title: Integrera ljud med senare bindning
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
