---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: Aktivera skärmfångst
title: Aktivera skärmfångst
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Aktivera skärmfångst{#enable-screen-capture}

TVSDK tillåter inte skärmfångst som standard. Spelaren anropar `setSecure(true)` objektet `com.adobe.ave.VideoEngineView` under konstruktionsfasen. Du har åtkomst till det här objektet eftersom du måste skapa ett `VideoEngineView` objekt och skicka det till `VideoEngine` objektet.

Så här aktiverar du skärmfångst i din app:

1. Skapa `com.adobe.ave.VideoEngineView` objektet.
1. Ring `setSecure(false)` på ditt `VideoEngineView` objekt.
