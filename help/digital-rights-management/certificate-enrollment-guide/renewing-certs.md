---
title: Förnya certifikat
description: Förnya certifikat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Förnya certifikat{#renew-certificates}

Du bör vara medveten om följande begränsningar för certifikatförnyelse som baseras på din Adobe Primetime DRM SDK-konfiguration:

* Primetime DRM Production SDK

   Adobe tillhandahåller den första uppsättningen kostnadsfria certifikat för Primetime DRM Production SDK när du köper ett supportavtal. Om du inte har något supportavtal kan du köpa en uppsättning förnyelsecertifikat som är giltiga i två år.
* Primetime DRM Evaluation SDK

   Certifikatet för SDK är giltigt i ett år och kan inte förnyas.
* Primetime DRM Trial SDK

   Testversionen av Primetime DRM SDK är giltig i tre månader och Adobe tillhandahåller en uppsättning kostnadsfria förnyelsecertifikat.

## Implementera nya certifikat och använda gamla certifikat för befintligt innehåll {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

I Primetime DRM kan du tillåta en licensserver att utfärda en licens för innehåll som paketerats med tidigare (eller t.o.m. utgångna) paketerarcertifikat. Om du vill konfigurera servern så att den accepterar licensbegäranden från tidigare paketerat innehåll, ska du tillhandahålla ditt gamla certifikat till servern och uppdatera serverns konfigurationsfil så att servern vet var de gamla certifikaten finns. Mer information finns i *Hantera certifikatuppdateringar när certifikat som utfärdas av Adobe upphör* i *Använda Adobe Primetime DRM SDK för att skydda innehåll*.

Om serverprogrammet baseras på implementeringen av DRM-referensen i Primetime behöver du inte uppdatera programmet på serversidan. I `flashaccess-refimpl.properties`-filen finns det fält där du kan ange ytterligare Transport- och License Server-certifikat. Om du bara har ett certifikat behöver du inte fylla i dessa egenskaper. Om du har upphört att gälla för certifikat och vill använda dessa certifikat när du utfärdar licenssvar, måste du tillhandahålla dessa certifikat till konfigurationsfilen och starta om servern.

Använd följande egenskaper för att ange gamla certifikat:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

