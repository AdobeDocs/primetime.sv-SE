---
keywords: setSecure;VideoEngineView
title: Aktivera skärmfångst
description: Aktivera skärmfångst
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Aktivera skärmfångst{#enable-screen-capture}

TVSDK tillåter inte skärmfångst som standard. Spelaren anropar `setSecure(true)` på `com.adobe.ave.VideoEngineView` objekt vid byggtid. Du har åtkomst till det här objektet eftersom du måste skapa en `VideoEngineView` -objektet och skicka det till `VideoEngine` -objekt.

Så här aktiverar du skärmfångst i din app:

1. Skapa `com.adobe.ave.VideoEngineView` -objekt.
1. Utlysning `setSecure(false)` på `VideoEngineView` -objekt.
