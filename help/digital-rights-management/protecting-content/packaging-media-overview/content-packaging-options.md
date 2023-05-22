---
title: Paketeringsalternativ
description: Paketeringsalternativ
copied-description: true
exl-id: 64c5c22d-0041-4fb9-80d0-72e11cb775f3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Paketeringsalternativ{#packaging-options}

Det finns många alternativ för att paketera innehåll. Du kan ange alternativ i dialogrutan `DRMParameters` gränssnitt och implementera de klasser som kan gränssnittet. Med dessa klasser kan du ange signatur- och nyckelparametrar samt ange om ljudinnehåll, videoinnehåll eller skriptdata ska krypteras. Om du vill se hur dessa implementeras i referensimplementeringen läser du beskrivningarna av kommandoradsalternativen för Media Packager i *Använda Adobe Primetime DRM Reference Implementations*. Dessa alternativ är baserade på Java API och är därför tillgängliga för programmatisk användning.

Paketeringsalternativen omfattar:

* Krypteringsalternativ (ljud, video, partiell kryptering).
* Licensserverns URL som klienten använder som bas-URL för alla begäranden som skickas till licensservern
* Transportcertifikat för licensserver
* Licensservercertifikat som används för att kryptera CEK
* Packager-autentiseringsuppgifter för signering av metadata
