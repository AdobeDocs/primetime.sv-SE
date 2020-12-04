---
description: Adobe Primetime DRM är en avancerad Digital Rights Management-lösning (DRM) och en lösning för innehållsskydd för högvärdigt audiovisuellt innehåll. I program som har stöd för att skapa Java API:er kan du använda Primetimes DRM SDK för att ange DRM-principer, tillämpa dessa principer på innehåll och kryptera innehållet.
seo-description: Adobe Primetime DRM är en avancerad Digital Rights Management-lösning (DRM) och en lösning för innehållsskydd för högvärdigt audiovisuellt innehåll. I program som har stöd för att skapa Java API:er kan du använda Primetimes DRM SDK för att ange DRM-principer, tillämpa dessa principer på innehåll och kryptera innehållet.
seo-title: Nyheter i Adobe Primetime DRM
title: Nyheter i Adobe Primetime DRM
uuid: 3c8da594-a231-4496-bffc-130775ecae50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Nyheter i Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM är en avancerad Digital Rights Management-lösning (DRM) och en lösning för innehållsskydd för högvärdigt audiovisuellt innehåll. I program som har stöd för att skapa Java API:er kan du använda Primetimes DRM SDK för att ange DRM-principer, tillämpa dessa principer på innehåll och kryptera innehållet.

>[!NOTE]
>
>Primetime DRM kallades tidigare Adobe Access och tidigare Flash Access.

Här är en genomgång av innehållsskyddsprocessen på hög nivå:

1. Använd API:erna för DRM Java för att ange DRM-principegenskaper och krypteringsparametrar.
1. Skapa en DRM-princip som beskriver användningsrollerna för allt innehåll.

   Du kan skapa valfritt antal DRM-profiler. De flesta användare skapar ett litet antal profiler och tillämpar dem sedan på många filer.
1. Paketera en mediefil.

   *`Packaging a file`* betyder att du krypterar filen och sedan tillämpar en DRM-profil på filen.
1. Implementera licensservern för att utfärda en licens till användaren.

När du har slutfört dessa steg är ditt krypterade innehåll klart för distribution. Efter distributionen kan klienten begära en licens från licensservern och vid mottagandet kan innehållet spelas upp.

Primetimes DRM SDK innehåller ett Java-API för att slutföra dessa åtgärder. SDK innehåller referensimplementeringar av licensservern och kommandoradsverktygen, som båda baseras på Java-API:erna för DRM SDK.

De funktioner som beskrivs nedan är nya i den här versionen.

## Nya funktioner {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Hårt stopp -** Du kan ange om uppspelningen ska stoppas eller fortsätta i slutet av uppspelningsfönstret.
* **Upplösningsberoende utdatakontroller -** Du kan ange utdatabegränsningar baserat på pixelupplösningar.
* **Anonymisering av licensserversvar -** För att öka integriteten med Primetimes DRM-licensserverprotokoll nollställs transportcertifikatets serienummer för licensserversvar till klienter som stöds.

