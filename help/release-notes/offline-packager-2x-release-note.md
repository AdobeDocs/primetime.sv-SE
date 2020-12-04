---
title: Primetime Offline Packager 2.x-versioner
seo-title: Primetime Offline Packager 2.x-versioner
description: Nyheter i Primetime Offline Packager 2.1 och 2.3.1
seo-description: Nyheter i Primetime Offline Packager 2.1 och 2.3.1
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---


# Primetime Offline Packager släpper {#primetime-offline-packager-x-releases}

Nyheter i Primetime Offline Packager 2.1 och 2.3.1

## Nyheter i Primetime Offline Packager 2.3.1 (oktober 2016) {#what-s-new-in-primetime-offline-packager-oct}

Versionen aktiverar On-demand-profil för MPEG-DASH, lägger till stöd för alternativet `validate` för PlaylistCreator och har få nyckelkorrigeringar för Multi-DRM-scenarier som listas nedan.

| **Utfärdningsnummer** | **Beskrivning** |
|---|---|
| PTPUB-985 | HLS AXS och Sample-AES fungerar inte för paketerargenererade nycklar |
| PTPUB-973 | Ett fel i krypteringsalgoritmen för visst Widewin-innehåll har korrigerats |
| PTPUB-964 | CENC-kryptering har brutits för vissa medietyper på vissa spelare - Android TVSDK. |
| PTPUB-954 | Sample-AES-kryptering åsidosätter AXS DRM som standard/Fel som inträffar när fjärrnyckelleverans är aktiverad. |
| PTPUB-951 | Offlinepaketeraren genererar inget undantag när key_file_path inte har angetts med Widewin. Det orsakar NPE i stället. |

Den senaste dokumentationen för Primetime Packagers finns på [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Känt fel i version 2.3.1 {#known-issue-in-version}

Följande problem finns i den här versionen.

| **Utfärdningsnummer** | **Beskrivning** |
|---|---|
| PTPUB-1005 | PlaylistCreator har inte rätt URL för .pssh-filen i den sista .mpd-filen som genererats för AAXS DRM. |
| PTPUB-1001 | PlaylistCreator ska generera ett fel när en tom sökväg anges via parametern in_path |
| PTPUB-990 | För DASH skriver inte Offline Packager genererad IV till disk när parametrarna `log_vi` &amp; `iv_out_path` har angetts. |
| PTPUB-980 | När konfigurationsfilen används för paketering tar inte parametern `key_url` bort citattecknen från angivna indata. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Lägsta systemkrav {#minimum-system-requirements}

Operativsystem som stöds

* Linux CentOS 6.3 64 bitar

Maskinvarukrav

* 3,2 GHz Intel® Pentium® 4-processor (Dual Intel Xeon® eller snabbare rekommenderas)

* 64-bitars operativsystem: 4 GB RAM (8 GB rekommenderas)

* Hårddisk

(Disk-SAS): Minst 10 GB med 7 500 v/min

(Disk-SSD): 400 MB/s läs-/skrivhastighet

(NAS): 1 GB dedikerad länk

Programvarukrav

* Oracle Java SE 1.8 eller senare

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Hämta Java SE från [Oracle webbplats](https://www.oracle.com/technetwork/java/javase/downloads/index.html) och följ installationsanvisningarna.
1. Extrahera Adobe Primetime Offline Packager 2.3.1-arkivfilen `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` till disken.

### Konfigurera Offline Packager 2.3.1 {#configuring-the-offline-packager}

Konfigurationsinstruktionerna finns i guiden Komma igång för Primetime Offline Packager på [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Nyheter i Primetime Offline Packager 2.1 (juli 2015) {#what-s-new-in-primetime-offline-packager-july}

Stöd för PlayReady BuyDRM (för DASH). Mer information finns i hjälpdokumentationen [som är tillgänglig här](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

Följande förbättringar har också gjorts i offlinepaketeraren.

PTPUB-780 Stöd för taggen EXT-X-START har lagts till

## Nyheter i Primetime Offline Packager 2.0 (juni 2015) {#what-s-new-in-primetime-offline-packager-june}

Stöd för rensa DASH-utdata har lagts till. Mer information finns i produktdokumentationen [här](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

Följande problem har också åtgärdats i den här versionen.

* PTPUB-783 Offline Packager kan nu hantera tomma WebVTT-filer.
* PTPUB- 781 Artifakter i HLS-utdata i Chrome när vissa omkodade MP4-resurser paketeras med offlinepaketerare för att producera MBR-utdata.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Lägsta systemkrav {#minimum-system-requirements-1}

**Operativsystem som stöds**

* Linux CentOS 6.3 64 bitar

**Maskinvarukrav**

* 3,2 GHz Intel® Pentium® 4-processor (Dual Intel Xeon® eller snabbare rekommenderas)

* 64-bitars operativsystem: 4 GB RAM (8 GB rekommenderas)

* 1 Gbit Ethernet-kort rekommenderas (flera nätverkskort och 10 Gbit stöds också)

* Hårddisk

   * (Disk-SAS): Minst 10 GB med 7 500 v/min
   * (Disk-SSD): 400 MB/s läs-/skrivhastighet
   * (NAS): 1 GB dedikerad länk

**Programvarukrav**

* Oracle Java SE 1.8 eller senare

### Installerar offlinepaketeraren 2.1 {#installing-offline-packager}

1. Hämta Java SE från [Oracle webbplats](https://www.oracle.com/technetwork/java/javase/downloads/index.html) och följ installationsanvisningarna.
1. Extrahera `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip` till disken.

### Konfigurera Offline Packager 2.1 {#configuring-the-offline-packager-1}

Information om konfigurationen som är tillgänglig här: [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.