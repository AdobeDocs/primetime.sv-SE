---
description: Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.
seo-description: Du kan integrera ljudströmmar med senare bindning eller alternativa ljudformat i spelaren genom att skapa en alternativ ljudfunktionshanterare.
seo-title: Integrera ljud med senare bindning
title: Integrera ljud med senare bindning
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '92'
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

