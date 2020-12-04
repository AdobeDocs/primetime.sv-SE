---
seo-title: Paketeringsalternativ
title: Paketeringsalternativ
uuid: 04244428-cb42-438a-8f16-91532c70ea60
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Paketeringsalternativ{#packaging-options}

Det finns många alternativ för att paketera innehåll. Du kan ange alternativen i gränssnittet `DRMParameters` och implementera klasserna som kan gränssnittet. Med dessa klasser kan du ange signatur- och nyckelparametrar samt ange om ljudinnehåll, videoinnehåll eller skriptdata ska krypteras. Om du vill se hur dessa implementeras i referensimplementeringen läser du beskrivningarna av kommandoradsalternativen för Media Packager som beskrivs i *Använda Adobe Primetime DRM Reference Implementations*. Dessa alternativ är baserade på Java API och är därför tillgängliga för programmatisk användning.

Paketeringsalternativen omfattar:

* Krypteringsalternativ (ljud, video, partiell kryptering).
* Licensserverns URL som klienten använder som bas-URL för alla begäranden som skickas till licensservern
* Transportcertifikat för licensserver
* Licensservercertifikat som används för att kryptera CEK
* Packager-autentiseringsuppgifter för signering av metadata

