---
seo-title: Terminologi och centrala begrepp
title: Terminologi och centrala begrepp
uuid: dc269873-7b63-4c18-bada-5338f4da0edd
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Terminologi och centrala begrepp{#terminology-and-core-concepts}

Följande termer och begrepp används i hela dokumentet:

**Konsument**

Konsumenten *är den* slutanvändare som laddar ned eller direktuppspelar innehåll.

**Innehåll**

*Innehållet* består av digitala ljud- eller videofiler.

**Innehållskrypteringsnyckel**

CEK ( *Content Encryption Key* ) är en krypteringsnyckel som används för att kryptera innehållet.

**Innehållsägare**

*Innehållsägare* är de företag som äger upphovsrätten till innehållet. Dessa kan vara stora filmstudior eller mindre, oberoende filmproducenter eller andra audiovisuella verk.

**Innehållspaket**

*Innehållspaket* är organisationer som paketerar innehåll för användning med Adobe Primetime DRM. Innehållsägare eller distributörer kan välja att paketera sitt eget innehåll eller registrera tjänster från en tredje part för att paketera sitt innehåll och distribuera det elektroniskt via Internet.

**Digitalt certifikat**

*Digitala certifikat* (kallas även *certifikat*) binder en enhet, till exempel en individ, organisation eller system, till ett specifikt nyckelpar för offentlig och privat nyckel. Digitala certifikat kan ses som elektroniska referenser som verifierar identiteten hos en individ, ett system eller en organisation.

**Digital signatur**

En *digital signatur* binder utgivarens identitet till innehållet som de har publicerat och tillhandahåller en mekanism för att upptäcka manipulering. Algoritmer för digitala signaturer använder kryptografiska hash-funktioner och asymmetriska - eller publika/privata nyckelpar - krypteringsalgoritmer. Vissa digitala signaturer utnyttjar också digitala certifikat och infrastruktur för publika nycklar (PKI) för att binda publika nycklar till identiteterna för innehållsägare eller distributörer.

**Distributör**

*Distributörer* (även kallade *innehållsdistributörer* eller* återförsäljare*) är företag som säkrar distributionsrättigheterna för att publicera och distribuera innehåll till konsumenter. I vissa fall är samma enhet både innehållsägare och innehållsdistributör.

**DRM-metadata**

Information som klienten (Adobe® Flash® Player, Adobe® AIR® runtime och Primetime client) skickar för att identifiera det begärda innehållet.

**Licens**

En *licens *är en datastruktur som innehåller en krypterad nyckel som används för att dekryptera innehåll som är kopplat till en profil. Licensen genereras av Primetime DRM när kunden begär innehåll och är bunden till konsumentens dator. Med hjälp av en policy som referens definierar licensen de rättigheter som är tillgängliga för den konsument som hämtar innehåll. För att kunna se innehållet måste konsumenten få en licens.

**Licenshämtning**

*Licenshämtning* innebär att man köper en licens som gör det möjligt för konsumenten att dekryptera och visa skyddat innehåll enligt en uppsättning användningsregler. Licenshämtning sker när en kund skickar information som identifierar det begärda innehållet ( *DRM-metadata*) och datorcertifikatet (identifierar konsumentens dator) till licensservern (se nedan).

**Licensserver**

License Server *kan integreras i distributörens eller tjänsteleverantörens fakturerings- och autentiseringssystem och kan innehålla affärslogik för att verifiera att den konsument som begär skyddat innehåll har behörighet att visa innehållet. Om användaren har behörighet att komma åt innehållet utfärdar licensservern en licens som tillåter körningsklienten att dekryptera och spela upp innehåll baserat på policyn och rättigheterna som är kopplade till konsumentens konto.

Du måste skapa och distribuera en licensserver med hjälp av Primetimes DRM SDK.

**Policy**

En *princip* är en behållare för användningsreglerna som avgör hur konsumenter kan använda skyddat innehåll. Profiler definieras oberoende av vilket innehåll som skyddas. En profil tillämpar inte rättigheter förrän den är bunden till innehållet via licensen. En policy listar de användarregler som innebär de behörigheter eller&quot;rättigheter&quot; som konsumenterna har till det innehåll de köper. Innehållsägare kan till exempel skapa en policy som ser till att skyddat innehåll endast är tillgängligt för konsumenter under en viss tidsperiod. Den här principen tillämpas sedan på allt innehåll som innehållsägaren vill tillämpa den här begränsningen för.

Principer skapas med Primetime DRM SDK.

**Skyddat innehåll**

*Skyddat innehåll* (även kallat *paketerat innehåll*) avser videoinnehåll som har krypterats med Primetime DRM SDK eller andra verktyg som stöds.

**Återförsäljare**

Se informationen för *distributörer* tidigare i det här avsnittet.
