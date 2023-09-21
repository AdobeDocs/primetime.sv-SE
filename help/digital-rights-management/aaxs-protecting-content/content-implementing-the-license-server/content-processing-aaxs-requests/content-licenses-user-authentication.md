---
title: Användarautentisering
description: Användarautentisering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Användarautentisering{#user-authentication}

En Adobe Access-begäran kan innehålla en autentiseringstoken.

Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genereras av `AuthenticationHandler`. Om du vill komma åt och verifiera token använder du `RequestMessageBase.getAuthenticationToken()`. Om du vill initiera en begäran om användarnamn/lösenord på klienten använder du `DRMManager.authenticate()` ActionScript eller iOS API.

Om klienten och servern använder en anpassad autentiseringsmekanism hämtar klienten en autentiseringstoken via någon annan kanal och ställer in den anpassade autentiseringstoken med `DRMManager.setAuthenticationToken` ActionScript 3.0 API. Använd `RequestMessageBase.getRawAuthenticationToken()` för att hämta den anpassade autentiseringstoken. Serverimplementeringen avgör om den anpassade autentiseringstoken är giltig eller inte.
