---
title: Distributionsalternativ för licensserver
description: Distributionsalternativ för licensserver
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Distributionsalternativ för licensserver{#license-server-deployment-options}

Du kan distribuera licensservern med något av följande alternativ:

* Adobe Primetime DRM Server for Protected Streaming - Denna licensserver är optimerad för direktuppspelning. Du kan till exempel konfigurera servern för Adobe HTTP Dynamic Streaming med Primetime DRM. Den här servern kan driftsättas enkelt med mycket liten konfiguration och har stöd för flera klientorganisationer. Den kan uppnå en hög nivå av skalbarhet. Eftersom den här implementeringen är optimerad för direktuppspelning stöder den inte alla DRM-funktioner i Primetime. Användarnamn/lösenord-autentisering, domäner och licenssammanlänkning stöds till exempel inte. Användningsreglerna i licenser som utfärdas av den här servern styrs av en serverkonfigurationsfil, som åsidosätter principen som används vid paketeringen.

  Se *Adobe Primetime DRM Server for Protected Streaming Guide* om du vill ha mer information om de användningsregler som stöds av licensservern.
* Referensimplementeringslicensserver - Du kan använda den här konfigurationen för att anpassa serverimplementeringen. Detta är ett exempel på en licensserverimplementering, inklusive källkod, som visar hur du använder API:erna i Primetimes DRM SDK för att hantera alla typer av begäranden och hur du implementerar anpassad affärslogik som stöds av en databas. Användningsreglerna i licenser som utfärdas av den här servern styrs av den princip som är kopplad till innehållet vid paketeringen.
* Anpassad serverimplementering - Du kan även implementera en egen licensserver med SDK. Informationen beskriver hur API:erna används för att implementera en licensserver.
