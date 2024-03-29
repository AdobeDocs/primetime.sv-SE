---
title: Terminologi och centrala begrepp
description: Terminologi och centrala begrepp
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Terminologi och centrala begrepp{#terminology-and-core-concepts}

Följande termer och begrepp används i hela dokumentet:

**Konsument**

The *konsument* är slutanvändaren som hämtar eller direktuppspelar innehåll.

**Innehåll**

*Innehåll* består av digitala ljud- eller videofiler.

**Innehållskrypteringsnyckel**

The *Innehållskrypteringsnyckel* (CEK) är en krypteringsnyckel som används för att kryptera innehållet.

**Innehållsägare**

*Innehållsägare* är de företag som äger upphovsrätten till innehållet. Dessa kan vara stora filmstudior eller mindre, oberoende filmproducenter eller andra audiovisuella verk.

**Innehållspaket**

*Innehållspaket* är organisationer som paketerar innehåll för användning med Adobe Primetime DRM. Innehållsägare eller distributörer kan välja att paketera sitt eget innehåll eller registrera tjänster från en tredje part för att paketera sitt innehåll och distribuera det elektroniskt via Internet.

**Digitalt certifikat**

*Digitala certifikat* (kallas även *certifikat*) binda en enhet, till exempel en individ, organisation eller system, till ett specifikt nyckelpar för offentlig och privat nyckel. Digitala certifikat kan ses som elektroniska referenser som verifierar identiteten hos en individ, ett system eller en organisation.

**Digital signatur**

A *digital signatur* binder utgivarens identitet till innehållet som de har publicerat och tillhandahåller en mekanism för att upptäcka manipulering. Algoritmer för digitala signaturer använder kryptografiska hash-funktioner och asymmetriska - eller publika/privata nyckelpar - krypteringsalgoritmer. Vissa digitala signaturer utnyttjar också digitala certifikat och infrastruktur för publika nycklar (PKI) för att binda publika nycklar till identiteterna för innehållsägare eller distributörer.

**Distributör**

*Distributörer* (kallas även *innehållsdistributörer* eller* återförsäljare*) är affärsenheter som säkrar distributionsrättigheter från rättighetsinnehavare för att publicera och distribuera innehåll till konsumenter. I vissa fall är samma enhet både innehållsägare och innehållsdistributör.

**DRM-metadata**

Information som klienten (dvs. Adobe® Flash® Player, Adobe® AIR® runtime och Primetime) skickar för att identifiera det begärda innehållet.

**Licens**

En *licens *är en datastruktur som innehåller en krypterad nyckel som används för att dekryptera innehåll som är kopplat till en profil. Licensen genereras av Primetime DRM när kunden begär innehåll och är bunden till konsumentens dator. Med hjälp av en policy som referens definierar licensen de rättigheter som är tillgängliga för den konsument som hämtar innehåll. För att kunna se innehållet måste konsumenten få en licens.

**Licenshämtning**

*Licenshämtning* är processen att köpa en licens som gör det möjligt för konsumenten att dekryptera och visa skyddat innehåll i enlighet med en uppsättning användningsregler. Licenshämtning sker när en kund skickar information som identifierar det begärda innehållet ( *DRM-metadata*) och datorcertifikatet (som identifierar konsumentens dator) till licensservern (se nedan).

**Licensserver**

License Server *kan integreras i distributörens eller tjänsteleverantörens fakturerings- och autentiseringssystem och kan innehålla affärslogik för att verifiera att den konsument som begär skyddat innehåll har behörighet att visa innehållet. Om användaren har behörighet att komma åt innehållet utfärdar licensservern en licens som tillåter körningsklienten att dekryptera och spela upp innehåll baserat på den policy och de rättigheter som är kopplade till konsumentens konto.

Du måste skapa och distribuera en licensserver med hjälp av Primetimes DRM SDK.

**Policy**

A *policy* är en behållare för användningsreglerna som avgör hur konsumenter kan använda skyddat innehåll. Profiler definieras oberoende av vilket innehåll som skyddas. En profil tillämpar inte rättigheter förrän den är bunden till innehållet via licensen. En policy listar de användarregler som innebär de behörigheter eller&quot;rättigheter&quot; som konsumenterna har till det innehåll de köper. Innehållsägare kan till exempel skapa en policy som ser till att skyddat innehåll endast är tillgängligt för konsumenter under en viss tidsperiod. Den här principen tillämpas sedan på allt innehåll som innehållsägaren vill tillämpa den här begränsningen för.

Profiler skapas med Primetime DRM SDK.

**Skyddat innehåll**

*Skyddat innehåll* (kallas även *paketerat innehåll*) avser videoinnehåll som har krypterats med Primetime DRM SDK eller andra verktyg som stöds.

**Återförsäljare**

Se tävlingsbidraget för *distributörer* tidigare i det här avsnittet.
