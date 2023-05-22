---
title: Användarautentisering
description: Användarautentisering
copied-description: true
exl-id: a0dd7d81-2249-4845-94da-53b755d6cd7c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Användarautentisering{#user-authentication}

En Adobe Access-begäran kan innehålla en autentiseringstoken.

Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genereras av `AuthenticationHandler`. Om du vill komma åt och verifiera token använder du `RequestMessageBase.getAuthenticationToken()`. Använd kommandot `DRMManager.authenticate()` ActionScript eller iOS API.

Om klienten och servern använder en anpassad autentiseringsmekanism hämtar klienten en autentiseringstoken via någon annan kanal och ställer in den anpassade autentiseringstoken med `DRMManager.setAuthenticationToken` ActionScript 3.0 API. Använd `RequestMessageBase.getRawAuthenticationToken()` för att hämta den anpassade autentiseringstoken. Serverimplementeringen avgör om den anpassade autentiseringstoken är giltig eller inte.
