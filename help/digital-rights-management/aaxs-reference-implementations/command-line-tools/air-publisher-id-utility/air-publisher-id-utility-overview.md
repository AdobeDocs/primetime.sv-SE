---
seo-title: Översikt över verktyget AIR Publisher ID
title: Översikt över verktyget AIR Publisher ID
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Översikt över verktyget AIR Publisher ID {#air-publisher-id-utility-overview}

Som en del av processen att skapa en AIR-fil genererar AIR Developer Tool (ADT) ett utgivar-ID. Detta är en identifierare som är unik för det certifikat som används för att skapa AIR-filen. Om du återanvänder samma certifikat för flera AIR-program har de samma utgivar-ID. Verktyget AIR Publisher ID används för att beräkna utgivar-ID:t för ett AIR-program. AIR-versioner efter 1.5.2 skriver inte det genererade utgivar-ID:t till en fil, så det är nödvändigt att använda det här verktyget för att fastställa utgivar-ID:t om du använder en AIR-programvitlista.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Utgivar-ID, som används för att framtvinga vitlistor i AIR, är inte detsamma som det utgivar-ID som anges av programutgivaren i programmets [!DNL application.xml] fil.

