---
title: Versionsinformation om PTAI 21.11.1
description: Versionsinformationen för PTAI beskriver vad som är nytt eller ändrat, de lösta och kända problemen i Primetime Ad Insertion under 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: f4c6ef44c7f13bf8170a1f23a7ae8eba0171316a
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Versionsinformation om Primetime Ad Insertion 21.11.1

Versionsinformationen för Primetime Ad Insertion 21.xx.x beskriver vad som är nytt eller ändrat, vilka problem som har lösts och kända problem i Primetime Ad Insertion under 2021.

## Nyheter i PTAI 21.11.1

När: Tisdagen den 9 november 2021 från kl. 13.30 till kl. 04.30 Eastern Time

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] kan nu konfigureras per zon.

* Roku Trick Play stöds helt.

## Förbättringar och korrigeringar i tidigare versioner

### Version 21.10.1

När: Tisdagen den 12 oktober 2021 mellan kl. 7:45 och kl. 1:45 Eastern Time

* Konsoliderade servrar, eliminerade icke-produktion och icke-användbara servrar.

### Primetime Ad Insertion Maintenance-release

När: Tisdagen den 28 september 2021 från kl. 17.00 till kl. 18.00 Eastern Time

* Uppdateringar av belastningsutjämningsstacken från AWS Elastic Load Balancer till AWS Application Load Balancer för förbättrad funktionalitet och skalbarhet. Dessa belastningsutjämnare används för att dirigera och begära trafik till Auditude-serverdelen från Ad Insertion-lagret (SSAI/CSAI).

### Version 21.9.1

När: Tisdagen den 7 september 2021 från 02:30 till 05:30 Eastern Time

* Uppdateringar av infrastrukturkomponenter bakom Primetimes medlings- och rapporteringskomponenter i Ad Insertion (Primetime Ads GUI).

### Version 21.8.1

När: Tisdagen den 24 augusti 2021 från kl. 02:00 till kl. 05:00 Eastern Time

* Stöd för DASH Live-/Linear-strömmar (VOD stöds redan).

### Version 21.5.1

När: Onsdagen den 26 maj 2021 från kl. 3:30 till kl. 06:30 (östra tid)

**Ändringar**

* Stöd för den inaktuella segmenteringstypen 0x01 (UPID) för SCTE-baserade cue-format har lagts till.

* Ny telemetri har lagts till för kommande ändringar av instrumentpanelen.

### Version 21.4.1

**När:** Torsdag den 22 april 2021 mellan kl. 17.00 och 17.00 (östra tid)

**Ändringar**

* Begränsning av sessionsbegäran aktiveras för att skydda mot potentiella DDOS-attacker. Sessionerna begränsas till 10 begäranden per sekund, med ett tak på 100 begäranden i kö. Vi räknar inte med någon effekt för spelare som beter sig enligt HLS/DASH-specifikationerna.

* Andra förbättringar av underhåll och säkerhet

### Version 21.2.2

**När:** Tisdagen den 23 februari 2021 från kl. 13.00 till kl. 04.00 Eastern Time

**Ändringar**

* Stöd för infogning/synkronisering av EXT-X-IMAGE-STREAM-INF-strömmar i HLS-strömmar har lagts till. Funktionen aktiveras via en konfiguration på serversidan. Kontakta din tekniska kontorepresentant för att aktivera funktionen.

### Version 21.2.1

**När:** Onsdagen den 3 februari 2021 från kl. 13.00 till kl. 04.00 Eastern Time

**Ändringar**

* Stöd för optimering av DASH-utdata har lagts till: tidsbaserad nodkonsolidering.

### Version 21.1.2

**När:** Tisdagen den 19 januari 2021 från kl. 12.30 till kl. 08.30 Eastern Time

**Ändringar**

* Underhållsuppdatering: Uppgradering av Primetime Ad Insertion-kluster för backend-memcachen.

### Version 21.1.1

**När:** Onsdagen den 13 januari 2021 från 01:00 till 04:00 Eastern Time

**Ändringar**

* Stöd för filialer finns för SCTE35-baserade cue-format.
