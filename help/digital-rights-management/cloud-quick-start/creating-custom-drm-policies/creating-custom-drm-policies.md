---
seo-title: Skapa anpassade DRM-profiler (valfritt)
title: Skapa anpassade DRM-profiler (valfritt)
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Skapa anpassade DRM-profiler (valfritt){#create-custom-drm-policies-optional}

Primetimes DRM Protection Kit innehåller några förkonfigurerade profiler som kan användas under paketeringen. Om ytterligare principkonfigurationer önskas, till exempel en specifik SWF-rättighetslista, kan den inkluderade DRM-principhanteraren användas för att generera anpassade principer.

>[!NOTE]
>
>Alla profiler måste använda ANONYMOUS-autentisering (inte lösenord för användarnamn eller anpassat), oavsett om arbetsflödet för anpassad autentisering/tillstånd används eller inte.

Principhanteraren ingår i konfigurationsfilen, som har ändrats så att endast de konfigurerbara principalternativ som stöds av DRM-tjänsten i Primetime Cloud visas [!DNL flashaccesstools.properties] . Om du anger principalternativ som inte stöds av DRM-tjänsten i Primetime Cloud resulterar det i licensförvärvsfel. Mer information om hur du använder Primetime DRM Policy Manager finns i: [Implementeringar av Primetime DRM-referenser: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Om du vill skapa en ny profil uppdaterar du [!DNL flashaccesstools.properties] filen och använder sedan kommandot:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Skapa profiler dynamiskt för anpassad autentisering/tillstånd{#create-policies-dynamically-for-custom-auth-entitlement}

Om du använder anpassad autentisering/tillstånd för Primetime Cloud DRM och vill skapa en ny DRM-princip dynamiskt för varje licensbegäran (i stället för att hämta principer från en förgenererad pool), rekommenderar Adobe att du använder Primetime DRM Java SDK direkt. Det går snabbare att använda Java SDK direkt än [!DNL AdobePolicyManager.jar] verktyget, vilket automatiskt ger ut principfilen till disken, vilket medför I/O-diskpålägg.

Exempelkod med Java SDK finns i [!DNL /Primetime DRM PolicyManager/sampleCode/] katalogen med namnen [!DNL CreatePolicy.java] och [!DNL CreatePolicyWithOutputProtection.java]. Javadocs och dokumentation för Java SDK finns i [Översikt över Adobe Primetime DRM SDK](../../../digital-rights-management/drm-sdk-overview/overview.md)

Om du vill skapa och köra exemplen kopierar du .java-filerna till mappen ../libs/ och kör:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
