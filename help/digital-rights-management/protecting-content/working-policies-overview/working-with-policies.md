---
seo-title: Arbeta med DRM-principer - översikt
title: Arbeta med DRM-principer - översikt
uuid: 32423448-013c-4183-bea8-e14b6690abdb
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Översikt {#working-with-drm-policies-overview}

Innehållsleverantörer kan tillämpa DRM-principer på mediefiler med hjälp av Primetimes DRM SDK. Administratörer kan sedan skapa, visa information om och uppdatera DRM-principer med hjälp av principhanterings-API:er.

En *`DRM policy`* är en samling information som innehåller säkerhetsinställningar, autentiseringskrav och användarrättigheter. Principen definierar hur användare kan visa innehåll. DRM-profiler, kryptering och signering gör att innehållsleverantörer kan behålla kontrollen över sitt innehåll oavsett hur brett innehållet distribueras.

En DRM-princip fungerar som en mall som licensservern använder när den genererar en licens. En klient kan också hänvisa till DRM-principen innan den begär en licens för att avgöra om klienten måste fråga användaren om autentisering innan den skickar en licensbegäran till servern.

Du kan leverera skyddat innehåll med Adobe Flash Media Server eller en HTTP-server. Användare kan hämta och spela upp skyddat innehåll i anpassade spelare som skapats med Primetimes DRM SDK.

En DRM-princip anger en eller flera rättigheter som beviljas klienten. Vanligtvis innehåller en DRM-princip minst *`Play Right`*. Du kan också ange flera uppspelningsrättigheter, var och en med olika begränsningar. När klienten får en licens med flera uppspelningsrättigheter, används den första licensen som uppfyller alla begränsningar. Du kan till exempel använda olika inställningar för utdataskydd på olika plattformar.

Se `CreatePolicyWithOutputProtection.java` i katalogen Reference Implementation Command Line Tools [!DNL samples] för exempelkod som illustrerar det här exemplet.

Du kan utföra följande uppgifter med Primetimes API:er för DRM-principhantering:

* Skapa och uppdatera policyer
* Visa DRM-principinformation
* Hantera uppdateringslistor för DRM-principer

Mer information om Java API finns i *Primetime DRM API Reference*.

Mer information om Primetimes DRM Policy Manager finns i *Using the Primetime DRM Reference Implementations* Guide.
