---
seo-title: Användarautentisering
title: Användarautentisering
uuid: 5cbd76b9-ff64-4a4b-8cfd-54f05c04eaa3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Användarautentisering {#user-authentication}

En Adobe Primetime DRM-begäran kan innehålla en autentiseringstoken.

Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` som genererats av `AuthenticationHandler`. Om du vill komma åt och verifiera token måste du använda `RequestMessageBase.getAuthenticationToken()`. Använd API:t `DRMManager.authenticate()` ActionScript eller iOS om du vill initiera en begäran om användarnamn/lösenord på klienten.

Om klienten och servern använder en anpassad autentiseringsmekanism hämtar klienten en autentiseringstoken via någon annan kanal och ställer in den anpassade autentiseringstoken med API:t `DRMManager.setAuthenticationToken` ActionScript 3.0. Använd `RequestMessageBase.getRawAuthenticationToken()` för att hämta den anpassade autentiseringstoken. Serverimplementeringen avgör om den anpassade autentiseringstoken är giltig.
