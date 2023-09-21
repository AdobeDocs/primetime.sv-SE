---
keywords: setSecure;VideoEngineView
title: Aktivera skärmfångst
description: Aktivera skärmfångst
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Aktivera skärmfångst{#enable-screen-capture}

TVSDK tillåter inte skärmfångst som standard. Spelaren anropar `setSecure(true)` på `com.adobe.ave.VideoEngineView` objekt vid konstruktionstillfället. Du har åtkomst till det här objektet eftersom du måste skapa en `VideoEngineView` -objektet och skicka det till `VideoEngine` -objekt.

Så här aktiverar du skärmfångst i din app:

1. Skapa `com.adobe.ave.VideoEngineView` -objekt.
1. Utlysning `setSecure(false)` på `VideoEngineView` -objekt.
