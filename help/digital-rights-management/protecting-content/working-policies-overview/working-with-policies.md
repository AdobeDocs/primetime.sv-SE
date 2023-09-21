---
title: Arbeta med DRM-principer - översikt
description: Arbeta med DRM-principer - översikt
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Ökning {#working-with-drm-policies-overview}

Innehållsleverantörer kan tillämpa DRM-principer på mediefiler med hjälp av Primetimes DRM SDK. Administratörer kan sedan skapa, visa information om och uppdatera DRM-principer med hjälp av principhanterings-API:er.

A *`DRM policy`* är en samling information som innehåller säkerhetsinställningar, autentiseringskrav och användarrättigheter. Principen definierar hur användare kan visa innehåll. DRM-profiler, kryptering och signering gör att innehållsleverantörer kan behålla kontrollen över sitt innehåll oavsett hur brett innehållet distribueras.

En DRM-princip fungerar som en mall som licensservern använder när den genererar en licens. En klient kan också hänvisa till DRM-principen innan den begär en licens för att avgöra om klienten måste fråga användaren om autentisering innan den skickar en licensbegäran till servern.

Du kan leverera skyddat innehåll med Adobe Flash Media Server eller en HTTP-server. Användare kan hämta och spela upp skyddat innehåll i anpassade spelare som skapats med Primetimes DRM SDK.

En DRM-princip anger en eller flera rättigheter som beviljas klienten. En DRM-princip innehåller vanligtvis minst *`Play Right`*. Du kan också ange flera uppspelningsrättigheter, var och en med olika begränsningar. När klienten får en licens med flera uppspelningsrättigheter, används den första licensen som uppfyller alla begränsningar. Du kan till exempel använda olika inställningar för utdataskydd på olika plattformar.

Se `CreatePolicyWithOutputProtection.java` i kommandoradsverktygen för referensimplementering [!DNL samples] katalog för exempelkod som illustrerar det här exemplet.

Du kan utföra följande uppgifter med Primetimes API:er för DRM-principhantering:

* Skapa och uppdatera policyer
* Visa DRM-principinformation
* Hantera uppdateringslistor för DRM-principer

Se *API-referens för Primetime DRM* om du vill ha mer information om Java API.

Se *Använda implementeringar av DRM-referenser för Primetime* för information om Primetime DRM Policy Manager.
