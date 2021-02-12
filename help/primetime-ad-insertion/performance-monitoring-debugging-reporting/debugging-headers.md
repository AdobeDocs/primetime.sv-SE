---
title: Felsöka rubriker
description: null
translation-type: tm+mt
source-git-commit: 45e5c8e6144adf4a405bde7d8d19505b7ad549e0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 7%

---


# Felsökningshuvuden (X-ADBE-AI-X1) {#debugging-headers}

SSAI skickar HTTP-huvuden som kan användas för att samla in information och fastställa prestanda för produktionssessioner, som finns i rubriken X-ADBE-AI-X1.

Exempelrubrik:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

Beskrivningen av fälten är följande:

| Namn | Beskrivning | Exempel |
|--- |--- |--- |
| isActivePreroll | Om ett reklamsamtal om förregistrering skickades | 0 |
| isActiveMidroll | Anger om ett reklamsamtal om midroll-roll skickades | 3 |
| ID för begäran | Intern SSAI | 1594181097704 |
| Sessions-ID | Sessions-ID för begäran | 1512633-5ba9-49b8-a219-4f37e60d259c |
| Strömtyp | u=variant, l=live, v=vod | v |
| isBootstrap | Om den här begäran är ett Bootstrap-anrop | 0 |
| Antal annonsbrytningar | Totalt antal annonsbrytningar i det här manifestet | 3 |
| Total annonsbrytningstid | Annonsbrytningens längd (i sekunder) | 30 |
| Antal annonsanrop | Antal annonseringsanrop som skickats i den här begäran | 2 |
| Antal omdirigerade annonsanrop | Antal omdirigerade annonsanrop som skickats i denna begäran | 3 |
| Total varaktighet för annonsanrop | Total bearbetningstid för annonsanrop | 199 |
| Infogat annonsantal | Antal annonser som infogats i manifestet | 2 |
| Begärandetid för källmanifest | Tidsåtgång för att hämta innehåll | 185 |
| Total begärandetid | Total tid för att hämta innehåll och annonser | 497 |
| Hämtningstid för annonsmaterial (totalt) | Total tid för hämtning av annonsviter | 204 |
| Tid för hämtning av annonsmaterial (faktisk) | Faktisk tid för att hämta och manifest parallellt | 104 |
| Träffar i innehållscache | Antal cacheträffar för innehåll | 0 |
| Saknar innehållscache | Antal missar i innehållscachen | 3 |
| Cacheträff i annonsvolym | Antal cacheträffar i annonsmanifestet | 0 |
| Missa annonsmanifestcache | Antal fel i annonsmanifestens cache | 4 |