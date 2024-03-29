---
description: De flesta annonsörer behöver detaljerad information om när, hur länge och hur bra deras annonser har visats. Det effektivaste sättet är att låta klientspelaren skicka rapporter när annonserna spelas upp, men manifestservern har också stöd för annonsspårning på serversidan och hybridsidan.
title: Annonsspårning
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Annonsspårning {#ad-tracking}

De flesta annonsörer behöver detaljerad information om när, hur länge och hur bra deras annonser har visats. Det effektivaste sättet är att låta klientspelaren skicka rapporter när annonserna spelas upp, men manifestservern har också stöd för annonsspårning på serversidan och hybridsidan.

När klienten aktiverar och spårar anger den en av följande metoder:

* **Klientsida** Tillsammans med den sammanfogade spellistan skickar servern en JSON-, VMAP- eller in-manifest-struktur till klienten som anger spårningshändelser och URL:er. Den här metoden är IAB-kompatibel (Interactive Advertising Bureau)

* **Serversidan** Klienten deltar inte i annonsuppföljning. Servern skickar all annonsspårningsinformation som den kan. Spårningsdata beräknas bara på serversidan och kanske inte matchar uppspelningsaktiviteten på klientsidan. Om en slutanvändare till exempel inte ser hela annonsen, efter att segmenten har levererats, kommer servern fortfarande att se annonsen som spelad.

* **Hybrid** Detta är som spårning på klientsidan, men klienten skickar sina rapporter till manifestservern som skickar dem till rätt URL. Annonsörer får samma information som med spårning på klientsidan. I det här läget kan klienter som kör med begränsad Internetåtkomst användas.