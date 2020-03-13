---
seo-title: Användarautentisering
title: Användarautentisering
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Användarautentisering{#user-authentication}

En Adobe Access-begäran kan innehålla en autentiseringstoken.

Om autentisering av användarnamn/lösenord användes kan begäran innehålla en `AuthenticationToken` genererad av `AuthenticationHandler`. Använd `RequestMessageBase.getAuthenticationToken()`för att få åtkomst till och verifiera token. Om du vill initiera en begäran om användarnamn/lösenord på klienten använder du API:t för `DRMManager.authenticate()` ActionScript eller iOS.

Om klienten och servern använder en anpassad autentiseringsmekanism hämtar klienten en autentiseringstoken via någon annan kanal och ställer in den anpassade autentiseringstoken med API:t för `DRMManager.setAuthenticationToken` ActionScript 3.0. Använd `RequestMessageBase.getRawAuthenticationToken()` för att hämta den anpassade autentiseringstoken. Serverimplementeringen avgör om den anpassade autentiseringstoken är giltig eller inte.
