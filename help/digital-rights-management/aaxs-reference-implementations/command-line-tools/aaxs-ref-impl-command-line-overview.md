---
title: Kommandoradsverktyg för att paketera innehåll och skapa ändringslistor
description: Kommandoradsverktyg för att paketera innehåll och skapa ändringslistor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Kommandoradsverktyg för att paketera innehåll och skapa ändringslistor {#command-line-tools-for-packaging-content-revocation-lists}

Referensimplementeringen innehåller följande kommandoradsverktyg:

* Policy Manager: Ett verktyg för att skapa och hantera principer
* Listhanterare för principuppdatering: Ett verktyg för att skapa och visa listor för principuppdateringar
* Hanteraren för återkallningslistor: Ett verktyg för att skapa och visa återkallningslistor
* Media Packager: Ett verktyg för att skapa krypterade FLV- och F4V-filer
* AIR Publisher ID
* UtilityLicense Generator
* License Embedder

## Krav {#requirements}

Följande krav gäller för kommandoradsverktygen i referensimplementeringarna:

* Alla kommandoradsverktyg kräver Java 1.5 eller senare.
* Autentiseringsuppgifter för Packager och License Server (certifikat och lösenord) som utfärdas av Adobe. Du behöver autentiseringsuppgifter för att kryptera och signera videofiler, för att signera principuppdaterings- och återkallningslistor samt för att generera licenser i förväg.

>[!NOTE]
>
>På grund av ett Java-fel får argument som används på kommandoraden (t.ex. filnamn, principnamn eller beskrivningar) endast använda tecken från operativsystemets standardteckenuppsättning.

## Konfigurationsfil {#configuration-file}

Flera av kommandoradsverktygen kräver en konfigurationsfil som innehåller information om verktygen som ska användas för att tillämpa principer och kryptera filer.

Standardkonfigurationsfilen är [!DNL flashaccesstools.properties]. Den finns i arbetskatalogen, d.v.s. den katalog som du kör verktygen från (se Installera kommandoradsverktygen). Varje verktyg innehåller också ett alternativ ( `-c`) som gör att du kan peka på den konfigurationsfil som du vill använda om du inte vill använda standardinställningen.

Konfigurationsfilen använder Java-egenskapens filformat. Om värden för någon av egenskaperna innehåller specialtecken bör du tänka på följande begränsningar:

* Escape-omvända snedstreck med ytterligare ett omvänt snedstreck. Du kan till exempel ange [!DNL C:\credentials.pfx] -fil, ange den som [!DNL C:\\credentials.pfx] eller `C:/credentials.pfx`. Om du vill ange en fil på en nätverksserver anger du `\\\\server\\folder\\filename.pfx`.
* Konfigurationsfilen får bara innehålla Latin-1-tecken. Om du måste använda tecken som inte är latinska-1 ska du använda rätt Unicode-escape-sekvens (eventuellt med [!DNL native2ascii] som medföljer Java).

Ange värden för egenskaper i konfigurationsfilen innan du kör verktygen. För vissa kommandoradsverktyg kan du ange värden för vissa alternativ antingen via kommandoraden eller konfigurationsfilen. I dessa fall prioriteras värden som ställs in via kommandoraden framför värden i konfigurationsfilen.

## Installera kommandoradsverktygen  {#installing-the-command-line-tools}

Du kan kopiera de filer du behöver från [!DNL \Reference Implementation\Command Line Tools] på dvd-skivan som innehåller standardkatalogen [!DNL flashaccesstools.properties] konfigurationsfil och en [!DNL libs] som innehåller JAR-filerna för verktygen.

The [!DNL samples] -katalogen innehåller flera exempel på Java-källfiler som visar hur API:erna för Adobe Access SDK används. Använd [!DNL build-samples.xml] Ant script.
