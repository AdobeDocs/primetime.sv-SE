---
description: Alla förfrågningar om annonsinfogning använder samma URL-struktur och samma grundläggande frågeparametrar. Ytterligare frågeparametrar gör att manifestservern kan arbeta med olika klienter och situationer.
title: Begäranden om annonsinfogning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Begäranden om annonsinfogning {#requests-for-ad-insertion}

Alla förfrågningar om annonsinfogning använder samma URL-struktur och samma grundläggande frågeparametrar. Ytterligare frågeparametrar gör att manifestservern kan arbeta med olika klienter och situationer.

| Parameter | Beskrivning |
|--- |--- |
| u | Resurs-ID:t är en MD5-hash av adobe_request_id från Adobe Primetime annonsbeslutsmetadata. Tillhandahålls av din kontoansvarige på Adobe. |
| z | Zon-ID för tillgången som måste tillhandahållas Auditude. Tillhandahålls av din kontoansvarige på Adobe. |
| `__sid__` | Ett unikt ID som manifestservern använder för att generera sessions-ID. |

>[!NOTE]
>
>Parametern `__sid__` omges av två understreck.

Manifestservern underhåller sessioner för enskilda klienter eller grupper av klienter för att säkerställa att sekvenserna av API-interaktioner för olika klienter hålls åtskilda. `__sid__` som klienten skickar i bootstrap-URL:en till manifestservern måste vara unik i sin miljö. Manifestservern använder den för att skapa ett globalt unikt ID som returneras till klienten.

De återstående frågeparametrarna gäller olika klienter och situationer.