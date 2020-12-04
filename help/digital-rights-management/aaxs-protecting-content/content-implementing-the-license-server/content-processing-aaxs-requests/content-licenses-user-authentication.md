---
seo-title: Användarautentisering
title: Användarautentisering
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Användarautentisering{#user-authentication}

En Adobe Access-begäran kan innehålla en autentiseringstoken.

Om autentisering av användarnamn/lösenord användes kan begäran innehålla ett `AuthenticationToken` som genererats av `AuthenticationHandler`. Använd `RequestMessageBase.getAuthenticationToken()` om du vill komma åt och verifiera token. Använd API:t `DRMManager.authenticate()` ActionScript eller iOS om du vill initiera en begäran om användarnamn/lösenord på klienten.

Om klienten och servern använder en anpassad autentiseringsmekanism hämtar klienten en autentiseringstoken via någon annan kanal och ställer in den anpassade autentiseringstoken med API:t `DRMManager.setAuthenticationToken` ActionScript 3.0. Använd `RequestMessageBase.getRawAuthenticationToken()` för att hämta den anpassade autentiseringstoken. Serverimplementeringen avgör om den anpassade autentiseringstoken är giltig eller inte.
