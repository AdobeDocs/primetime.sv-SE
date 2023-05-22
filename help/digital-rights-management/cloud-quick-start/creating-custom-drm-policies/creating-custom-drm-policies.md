---
title: Skapa anpassade DRM-profiler (valfritt)
description: Skapa anpassade DRM-profiler (valfritt)
copied-description: true
exl-id: a74f60b1-96a0-4fc4-bbf2-5db78f343562
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Skapa anpassade DRM-profiler (valfritt){#create-custom-drm-policies-optional}

Primetimes DRM Protection Kit innehåller några förkonfigurerade profiler som kan användas under paketeringen. Om ytterligare principkonfigurationer önskas, till exempel en specifik listrättighet som tillåter SWF, kan den inkluderade DRM-principhanteraren användas för att generera anpassade principer.

>[!NOTE]
>
>Alla profiler måste använda ANONYMOUS-autentisering (inte lösenord för användarnamn eller anpassat), oavsett om arbetsflödet för anpassad autentisering/tillstånd används eller inte.

Policyhanteraren är [!DNL flashaccesstools.properties] konfigurationsfil, som har ändrats så att endast de konfigurerbara principalternativ som stöds av DRM-tjänsten i Primetime Cloud visas. Om du anger principalternativ som inte stöds av DRM-tjänsten i Primetime Cloud resulterar det i licensförvärvsfel. Mer information om hur du använder Primetime DRM Policy Manager finns i: [Implementeringar av Primetime DRM-referenser: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Om du vill skapa en ny profil uppdaterar du [!DNL flashaccesstools.properties] och använd sedan kommandot:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Skapa profiler dynamiskt för anpassad autentisering/tillstånd{#create-policies-dynamically-for-custom-auth-entitlement}

Om du använder anpassad autentisering/tillstånd för Primetime Cloud DRM och vill skapa en ny DRM-princip dynamiskt för varje licensbegäran (i stället för att hämta principer från en förgenererad pool), rekommenderar Adobe att du använder Primetime DRM Java SDK direkt. Det går snabbare att använda Java SDK direkt än [!DNL AdobePolicyManager.jar] som automatiskt matar ut principfilen till disk, vilket medför I/O-diskpålägg.

Exempelkod med Java SDK finns i [!DNL /Primetime DRM PolicyManager/sampleCode/] katalog, namngiven [!DNL CreatePolicy.java] och [!DNL CreatePolicyWithOutputProtection.java]. Javadocs och dokumentation för Java SDK finns på [En översikt över Adobe Primetime DRM SDK](../../../digital-rights-management/drm-sdk-overview/overview.md)

Om du vill skapa och köra exemplen kopierar du .java-filerna till mappen ../libs/ och kör:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
