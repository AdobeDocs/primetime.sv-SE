---
description: För att kunna implementera DRM behöver du särskilda certifikat och nycklar, inklusive en krypteringsnyckel eller CEK för att kryptera ditt innehåll, en kundautentiserare för att skydda kommunikationen med ExpressPlay-servrar och CEKSID för att identifiera dina krypteringsnycklar som sparade i ett nyckelhanteringssystem.
title: Tangenter, ID:n och autentiserare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Tangenter, ID:n och autentiserare{#keys-ids-and-authenticators}

För att kunna implementera DRM behöver du särskilda certifikat och nycklar, inklusive en krypteringsnyckel eller CEK för att kryptera ditt innehåll, en kundautentiserare för att skydda kommunikationen med ExpressPlay-servrar och CEKSID för att identifiera dina krypteringsnycklar som sparade i ett nyckelhanteringssystem.

Du behöver dessa objekt för att paketera, licensiera och spela upp skyddat innehåll:

## Innehållskrypteringsnyckel {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

CEK (Content Encryption Key) är en 16-byte-sträng som används för att kryptera innehåll.

**Vad är CEK?** - CEK är nyckeln som din paketerare använder för att kryptera ditt innehåll. Det är en 16 byte hex-kodad sträng.

**Var kommer CEK ifrån?** - Du (innehållsleverantören) skapar den här nyckeln själv med ett verktyg som OpenSSL eller Notepad++. Exempel:

```
openssl rand 16 -hex > cek_hex_file
```

eller (för Adobe Offline Packager):

1. Generera den 16 byte hex-kodade strängen enligt ovan eller med något annat verktyg. Det kommer att se ut ungefär så här:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Öppna Notepad++ och klistra in i 16 byte hex-strängen.
1. Konvertera det här värdet från hex ASCII med Base64-kodning för att skapa [!DNL keyfile.bin]. (Detta beskrivs i [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Samma nyckel, annat namn?** - Ja, du kan se det CK som andra namn hänvisar till på andra platser, som:

* ** [!DNL [någon fil].bin]** - Adobe Offline Packager refererar till CEK:n som [!DNL [någon fil].bin]; t.ex. * [!DNL Keyfile.bin]* - Detta är ditt CEK som det används av Adobe Offline Packager, i form av en fil på datorn som du använder för att paketera innehåll.

   Du&quot;Base64&quot; din slumpmässiga CEK-hexsträng och sparar den som en fil (t.ex. [!DNL keyfile.bin]), som vanligtvis finns i katalogen [!DNL creds] under [!DNL offlinepkgr/]. I Packager-konfigurationsfilen (du kan t.ex. kalla den [!DNL widevine.xml] om du packar för Widewin DRM) refererar du till ditt CEK i din konfigurationsfil så här:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Innehållsnyckel**  - Du kan även se CEK-värdet som kallas för innehållsnyckel vid samtal (  `&contentKey=`), i felmeddelanden, i supportärenden och i annan dokumentation.

**När / var ska jag använda den?**

1. Först måste du ha CEK tillgängligt på den dator där du packar. Ditt paketeringsverktyg använder ditt CEK för att kryptera ditt innehåll.
1. För det andra måste du lagra CEK i någon form av nyckelhanteringssystem (KMS), där varje CEK är associerat med sin egen [innehållskrypteringsnyckel](../../multi-drm-workflows/glossary/glossary-cek.md). Du kan skapa en egen KMS eller använda [ExpressPlays nyckellagringsutrymme](https://www.expressplay.com/developer/key-storage/). På så sätt kan din butik (din tillståndsserver, som hanterar kundernas berättigande och License Token-etablering) hämta en licenstoken för kunden från KMS med ett nyckel-ID i stället för det faktiska CEK-värdet (detta är mycket säkrare).

## Lagring-ID för innehållskrypteringsnyckel {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

CCEKSID (Content Encryption Key Storage ID) identifierar unikt den lagrade nyckel som dekrypterar ett krypterat videomaterial.

**Vad är CEKSID?** - CEKSID är den unika identifieraren för en innehållskrypteringsnyckel (CEK). CEK är nödvändigt för att låsa upp det skyddade innehållet. CEKSID är nödvändigt för att få tillgång till det CEK där det lagras. När du testar konfigurationen kan du tillhandahålla ett slumpmässigt CEKSID och CEK under paketeringstiden, förutsatt att du använder samma information för licensierings- och uppspelningskontrollerna.

**Var kommer den ifrån?** - Du (innehållsleverantören) kan skapa detta ID själv, eller du kan använda en tjänst som  [ExpressPlays Key ](https://www.expressplay.com/developer/key-storage/) Storage för att generera CEKSID för var och en av dina CEK (och lagra båda). Dessutom kan ni använda slumpmässigt genererade CEKSID:er eller använda ett schema som passar er affärsmodell. Du kan till exempel använda CEKSID som är meningsfulla strängar i stället för slumpmässiga Hex-strängar (ID-namnet kan bestå av ämnen, datum, tider osv.)

**Vad mer heter CEKSID?** - Det kallas ibland för ett  *innehålls-ID*.

## Kundens autentisering {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

Kundautentiseraren är en nyckel som du får från ExpressPlay när du skapar ett administratörskonto där. Autentiseraren används i kommunikation med ExpressPlay-servrar.

**Vilka är kundautentiserarna?** - De två kundautentiserarna består av de två ID:n - en för testning, en för produktion - som du registrerar för ExpressPlay när du registrerar dig för deras tjänst. De är alltid tillgängliga på din ExpressPlay-administratörssida:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**När använder jag den här?** - Detta ingår i alla anrop till ExpressPlay-servrar - till exempel licensservrar,  [ExpressPlay-nyckellagring](https://www.expressplay.com/developer/key-storage/) och andra samtal.
