---
title: Primetime Streaming Server-versioner
seo-title: Primetime Streaming Server 1.x-versioner
description: Nyheter i Primetime Streaming Server 1.3 och 1.4.
seo-description: Nyheter i Primetime Streaming Server 1.3 och 1.4.
uuid: be05db6b-713f-4406-940d-9f3a805f967b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: baec714e-9d41-4e8b-b134-13a736885cbd
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 0%

---


# Primetime Streaming Server-versioner {#primetime-streaming-server-x-releases}

Nyheter i Primetime Streaming Server 1.3 och 1.4.

## Nytt i Primetime Streaming Server 1.4 (december-utgåvan) {#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* Utdata-HLS-strömmar innehåller nu ID3-metadata i MPEG-2 TS
* HLS-ljudströmmar kan nu ha en associerad statisk bild
* Stöd för att tillhandahålla IV som användarindata för HLS AES-krypteringsarbetsflöden
* Stöd för att exportera IV till en fil när IV genereras av offlinepaketeraren
* Playlist Creator har nu stöd för att associera flerspråkiga ljudgrupper och flerspråkiga WebVTT-underrubriksgrupper med medieströmmar

**Ursprungsserver**

* HLS AES-kryptering är tillgängligt för Live- och VOD-arbetsflöden. Primetime Origin kan Just in Time använda HLS AES-kryptering på inkommande HLS-strömmar eller MP4-filer.
* Den kan också tillämpa JIT HLS AES-kryptering när den används för att konvertera inkommande HDS-strömmar till HLS-strömmar.
* Primetime Origin har nu stöd för att visa en lista över tillåtna SWF-flöden för PHLS-strömmar. Tidigare stöddes den bara för PHDS-strömmar

**Primetime Live Packager**

* Stöd för att generera HLS AES-128-strömmar för RTMP- och MPEG-2 TS-strömmar

PHDS/PHLS-certifikat har uppdaterats. Ett nytt förfallodatum för detta kommer att vara 2016-01-10.

### **Felkorrigeringar i version 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- HLS-manifestet på inställningsnivå som har skapats av OfflinePackager 1.3.1 saknar kodek- och upplösningsinformation.
* PTPUB-353 - PlayListCreator stöder inte tillägg av WebVTT-information i manifestet på uppsättningsnivån
* PTPUB-583 - Verktyget PlaylistCreator förskriver oväntat grupp-URI:er med.
* PTPUB-605 Playlist Creator not listing SUBTITLE Group in each variant stream
* PTPUB-634 -Offline Packager lägger till SpliceInsert i manifestet.
* PTPUB-635 - Flera SpliceOut-taggar infogade för en annonsreferens.

### Känt fel i version 1.4 {#known-issue-in-release}

* PTPUB-645 DPISimple Mode är tvångsmässigt även när DPIScte35-läge har angetts när både kommandoradsledd och cues i direktuppspelning finns i offlinepaketerkonfigurationen

## Nyheter i Primetime Streaming Server 1.3.1 (MAY Release) {#what-s-new-in-primetime-streaming-server-may-release}

Version 1.3.1 hänvisar till programfixen. Följande förbättringar gör den till en rekommenderad uppgradering för kunder eftersom den består av viktiga prestandaförbättringar för JIT MP4-användningsfall:

1. Prestandakorrigering för MP4 JIT m3u8-generering på origin med DRM inklusive nyckelrotation
1. En konfiguration med CopyQueryParamToJITFragmentURI:er har lagts till för att kopiera frågeparametrar från JIT-manifestbegäran till genererade fragment-URI:er för MP4 JIT-konvertering. Se dokumentationen för HTTP Origin Server för exempelanvändning
1. Tillåt MP4-filer utan filtillägg för JIT-konvertering via konfigurationen Config/MP4Only som lagts till i vod.xml

### Felkorrigeringar i version 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Alla SCTE35-tecken kan inte dirigera till utdatamanifestet på grund av tidsstämpelfel vid paketering. Använd pts_adjustment på SpliceTime i TimeSignal för SpliceInfoSection i SCTE35-meddelandet.

### Kända fel i version 1.3.1 {#known-issues-in-release}

* 3717039 - När paketeraren är konfigurerad för att producera enkla DPI-lägen bör den verkligen leta efter specifika signaltyper, t.ex. infogning av splice eller placeringsmöjligheter, och konvertera endast dessa till enkla läges-cues. Den bör ignorera andra typer av signaler som programstart, nätverksstart osv.

* 3718598 - När origin-servern är konfigurerad för att hantera skyddat innehåll med HSM-åtkomst aktiverad, sker en LunaSA-klient i serverdelen ofta kommunikation med HSM-modulen

## Nyheter i Primetime Streaming Server 1.3 (APRIL-version) {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3 innehåller flera nya funktioner för strömning av innehåll, bättre användbarhet och säkerhet.

**Primetime Streaming Server som en enhetlig form av Live Packager och origin Server**

Primetime Live Packager och Primetime Origin samlas ihop och fungerar som en enda komponent. Den här komponenten kan användas som en Packager eller som origin eller som en kombination av funktioner för att paketera och vara värd för en direktuppspelning.

Detta ger dessa servrar ett enhetligt filgränssnitt som gör dem enkla att köra på en enda dator. Den ger även fortsättningsvis flexibilitet att konfigureras som en separat Packager eller origin.

**Beta MPEG - DASH-stöd**

Primetime Streaming Server stöder MPEG-DASH-paketering för Live- och VOD-arbetsflöden. Live-paketerarkomponenten konverterar inkommande RTMP- eller MPEG-2-TS-strömmar till DASH-format. Origin-komponenten accepterar en DASH-ström.

För VOD-arbetsflöden konverterar offlinepaketerarkomponenten MP4- och TS-resurser till MPEG-DASH ISOBFF-format.

**Konvertering från live till VOD**

Det finns nu en ny komponentserver för inspelning som har stöd för att spela in en liveström och arkivera för VOD-uppspelning. Det har stöd för att skapa fullständiga händelseuppspelningar samt klipp/högdagrar för en del av händelsen. Den kan konfigureras för att spela in strömmar med endast ljud, ta bort annonser eller Slates i Live-innehåll. Inspelningsservern fungerar med Primetime Streaming Server och tredjeparts Origins.

**Konvertering av RTMP till HLS i Primetime Live Packager**

Primetimes Live Packager-komponent stöder skapande av HLS-strömmar från RTMP-strömmar. Det gör det också möjligt att lägga till Primetime DRM och Skyddad strömning till HLS-utdataströmmarna.

**Autentisering för inkommande RTMP-strömmar till Primetime Live Packager**

En usermgmt.jar levereras nu med Primetime Live Packager för att konfigurera åtkomst med betrodda autentiseringsuppgifter när en RTMP-ström skickas till Primetime Live Packager

Nu kan kodare konfigureras att använda ett användarnamn/lösenord när de skickar strömmar till Live Packager.

**PlaylistCreator Tool to create Top-Level manifest for HDS and HLS**

Det finns nu ett verktyg för PlaylistCreator.jar med Primetime Offline Packager som gör det enkelt att skapa manifestfiler på den högsta nivån för HDS- och HLS-resurser.

**Ytterligare säkerhetsfunktion som inkluderar en modul för maskinvarusäkerhet**

Primetime Offline Packager har nu stöd för åtkomst till Packager Credential Certificate och Common Keys från en maskinvarusäkerhetsmodul.

En modul för maskinvarusäkerhet ger ytterligare skydd för dessa konfidentiella tillgångar.

**Förbättrade prestanda för VOD-paketering**

Flera prestandaförbättringar har införts för att förbättra paketeringstiden för mezzanine-resurser i Primetime Offline Packager

**Förbättrade prestanda för JIT MP4-paketering**

Flera prestandaförbättringar har lagts till i JIT-paketeringsfunktionerna i Primetime Origin för att hantera användarförfrågningar för ett stort bibliotek med VOD-resurser.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Lägsta systemkrav {#minimum-system-requirements}

**Nätverkskrav**

* Nätverket ska vara multicast aktiverat för att skicka MPEG-TS-ström från en kodare till Live Packager. Live Packager accepterar även en RTMP-ström från en kodare som inte kräver något multicast-nätverk.

**Operativsystem som stöds**

* Linux CentOS 6.3 64 bitar

**Maskinvarukrav**

* 3,2 GHz Intel® Pentium® 4-processor (Dual Intel Xeon® eller snabbare rekommenderas)
* 64-bitars operativsystem: 4 GB RAM (8 GB rekommenderas)
* 1 Gbit Ethernet-kort rekommenderas (flera nätverkskort och 10 Gbit stöds också)
* Skiva:

   * (Disk-SAS): Minst 10 GB med 7 500 v/min
   * (Disk-SSD): 400 MB/s läs/skriv
   * (NAS): 1 GB dedikerad länk

**Programvarukrav**

* Oracle Java JRE 1.7 (rekommenderas: Sun/Oracle Hotspot-JVM). JDK krävs för JConsole-åtkomst till JMX API:er

### Installera och konfigurera Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Installera direktuppspelningsserver**

1. Hämta Java SE- och JDK-programvaran från [Oracle-webbplatsen](https://www.oracle.com/technetwork/java/javase/downloads/index.html) och följ installationsanvisningarna.
2. Extrahera arkivfilen Adobe Primetime-Streaming Server 1.4 `Primetime- StreamingServer-1-4-0-b206-12042014.zip` till hårddisken.

**Starta Primetime Streaming Server**

Du startar direktuppspelningsservern genom att köra följande kommando från kommandoraden i direktuppspelningsserverns rotkatalog:\
`$./pss_start.sh`

**Konfigurera Primetime Streaming Server som Live Packager eller HTTP Origin Server**

Om du vill konfigurera direktuppspelningsservern som Live Packager eller origin Server uppdaterar du konfigurationsfilen pss.xml som finns i conf-katalogen i strömningsserverns rotkatalog:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Stoppa Primetime Streaming Server**

Om du vill stoppa direktuppspelningsservern kör du följande kommando i direktuppspelningsserverns rotkatalog:\
`$./pss_stop.sh`

**Starta om Primetime Streaming Server**

Om du vill starta om direktuppspelningsservern stoppar du och startar direktuppspelningsservern.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Avinstallerar Primetime Streaming Server**

Om du vill avinstallera direktuppspelningsservern stoppar du direktuppspelningsservern och tar bort direktuppspelningsserverns pss-katalog i Primetime-katalogen

## Arbeta med Live Packager och origin Server 1.4 {#working-with-live-packager-and-origin-server}

Det här avsnittet gäller när Primetime Streaming Server inte används och istället distribueras Primetime Live Packager AND/OR Primetime Origin Server

### Lägsta systemkrav {#minimum-system-requirements-1}

**Nätverkskrav**

* Nätverket ska vara multicast aktiverat för att skicka MPEG-TS-ström från en kodare till Live Packager. Live Packager accepterar även en RTMP-ström från en kodare som inte kräver något multicast-nätverk.

**Operativsystem som stöds**

* Linux CentOS 6.3 64 bitar

**Maskinvarukrav**

* 3,2 GHz Intel® Pentium® 4-processor (Dual Intel Xeon® eller snabbare rekommenderas)
* 64-bitars operativsystem: 4 GB RAM (8 GB rekommenderas)
* 1 Gbit Ethernet-kort rekommenderas (flera nätverkskort och 10 Gbit stöds också)
* Skiva:

   * (Disk-SAS): Minst 10 GB med 7 500 v/min
   * (Disk-SSD): 400 MB/s läs/skriv
   * (NAS): 1 GB dedikerad länk

**Programvarukrav**

* Oracle Java JRE 1.7 (rekommenderas: Sun/Oracle Hotspot-JVM). JDK krävs för JConsole-åtkomst till JMX API:er

Systemkraven ovan gäller både origin-servern och Live Packager.

### Installera och konfigurera Live Packager {#install-and-configure-the-live-packager}

**Installera Live Packager**

1. Hämta Java SE- och JDK-programvaran från [Oracle-webbplatsen](https://www.oracle.com/technetwork/java/javase/downloads/index.html) och följ installationsanvisningarna.
1. Extrahera arkivfilen Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` till hårddisken.

**Installerar HTTP Origin Server**

1. Hämta Java JRE och JDK från [Oracles webbplats](https://www.oracle.com/technetwork/java/javase/downloads/index.html) och följ installationsanvisningarna.
1. Extrahera arkivfilen Adobe Primetime - HTTP Origin Server 1.4 `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`till hårddisken.

**Starta Live Packager** Starta paketeraren genom att köra följande kommando från paketerarens rotkatalog:\
`$packager_start.sh`

**Starta HTTP Origin Server**

Du startar HTTP Origin Server genom att köra följande kommando från kommandoraden i origin-serverns rotkatalog:\
`$./origin_start.sh`

**Stoppa Live Packager**

Om du vill stoppa paketeraren kör du följande kommando från paketerarens rotkatalog:\
`$packager_stop.sh`

**Stoppa HTTP Origin-servern**

Om du vill stoppa HTTP Origin Server kör du följande kommando i origin-serverns rotkatalog:\
`$./origin_stop.sh`

**Starta om Live Packager**

Starta om paketeraren genom att stoppa och starta paketeraren.

**Obs**: När paketeraren startas försöker den initiera bootstrap-informationen från fragmentmålet i den tillfälliga katalogen. Om bootstrap-informationen hittas vid fragmentmålet betyder det att paketeraren har startats om. Vid omstart väntar paketeraren tills nästa fragmentgräns nås och börjar sedan paketera. Paketeraren infogar en mellanrumspost i bootstrap för att ange att det saknas fragment.

**Starta om HTTP Origin Server**

Starta om HTTP Origin Server genom att stoppa och starta HTTP Origin Server.

**Konfigurera Live Packager**

Distributionsfilen innehåller en exempelkonfiguration som kan användas för att testa paketeraren.

När du har extraherat Adobe Primetime - Live Packager 1.4-arkivet ändrar du kataloger till paketerarkatalogen och kör skriptet packager_start.sh. Exempelkonfigurationen lyssnar på multicast-adressen 239.235.0.3:14000 och kör den lokala origin-servern på port 8080. Utdata är konfigurerade att skrivas till `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Konfigurera HTTP Origin Server**

Information om konfigurationen som finns här finns i dokumentet Komma igång för Primetimes HTTP Origin Server.

**Live Packager avinstalleras**

Om du vill avinstallera paketeraren stoppar du paketeraren och tar bort paketerarkatalogen från Primetime-katalogen.

**Avinstallerar HTTP Origin Server**

Om du vill avinstallera HTTP Origin Server stoppar du HTTP Origin Server och tar bort HTTP Origin Servers httport-katalog i Primetime-katalogen.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Lägsta systemkrav {#minimum-system-requirements-2}

**Operativsystem som stöds**

* Linux CentOS 6.3 64 bitar

**Maskinvarukrav**

* 3,2 GHz Intel® Pentium® 4-processor (Dual Intel Xeon® eller snabbare rekommenderas)
* 64-bitars operativsystem: 4 GB RAM (8 GB rekommenderas)
* 1 Gbit Ethernet-kort rekommenderas (flera nätverkskort och 10 Gbit stöds också)
* Skiva:

   * (Disk-SAS): Minst 10 GB med 7 500 v/min
   * (Disk-SSD): 400 MB/s läs/skriv
   * (NAS): 1 GB dedikerad länk

**Programvarukrav**

* Oracle Java JRE 1.7 eller senare.

### Installera och konfigurera offlinepaketeraren {#install-and-configure-offline-packager}

Så här installerar du Offline Packager:

1. Ladda ned Java SE från [Oracles webbplats](https://www.oracle.com/technetwork/java/javase/downloads/index.html) och följ installationsanvisningarna.
1. Extrahera arkivfilen Adobe Primetime - Offline Packager 1.4 `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`till hårddisken.

Information om konfigurationen som är tillgänglig [här](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)finns i dokumentet Komma igång för Primetime Offline Packager.

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetimes sida för utbildning och support](https://helpx.adobe.com/support/primetime.html) .