---
keywords: setSecure;VideoEngineView
title: Aktivera skärmfångst
description: Aktivera skärmfångst
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Aktivera skärmfångst{#enable-screen-capture}

TVSDK tillåter inte skärmfångst som standard. Spelaren anropar `setSecure(true)` på `com.adobe.ave.VideoEngineView`-objektet under konstruktionstiden. Du har åtkomst till det här objektet eftersom du måste skapa ett `VideoEngineView`-objekt och skicka det till `VideoEngine`-objektet.

Så här aktiverar du skärmfångst i din app:

1. Skapa `com.adobe.ave.VideoEngineView`-objektet.
1. Anropa `setSecure(false)` på ditt `VideoEngineView`-objekt.
