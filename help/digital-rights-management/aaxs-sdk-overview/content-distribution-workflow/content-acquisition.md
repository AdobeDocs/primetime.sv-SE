---
title: Inköp av innehåll
description: Inköp av innehåll
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Inköp av innehåll {#content-acquisition}

När en konsument köper en skyddad innehållsfil från en webbplats eller ett CDN-nummer måste konsumenten också skaffa en licens som innehåller en nyckel för att dekryptera videon innan den kan spelas upp. Följande steg illustrerar ett vanligt arbetsflöde för hur skyddat innehåll används av en dator som kör Flash Player eller Adobe AIR:

1. Konsumenten besöker butikens webbplats och väljer en video att titta på. Konsumenten försöker hämta eller strömma den skyddade videon till sin dator med antingen Flash Player eller ett Adobe AIR-program.

   Om detta är första gången som konsumenten försöker få åtkomst till skyddat innehåll med den här specifika datorn måste Flashen Player eller Adobe AIR-miljön först individualiseras enligt beskrivningen i steg 2. Om runtime-klienten redan har anpassats individuellt utförs processen att skaffa en licens enligt beskrivningen i steg 3.

1. Flashen Player eller Adobe AIR runtime-klienten får ett unikt digitalt certifikat (kallas *datorcertifikat*) från en värdserver i Adobe.

   Den här processen att tilldela ett unikt certifikat anropas *individualisering*. Individualisering är en unik identifiering av både den dator och den Flash Player eller den Adobe AIR-miljö som används för att spela upp innehåll.

   I personaliseringsprocessen kan de hämtade licenserna bindas till en specifik dator där klienten är installerad. Varje dator får en unik datorreferens (datorns privata nyckel och datorcertifikat). Om en viss kund skulle bli komprometterad kan den återkallas och förhindras från att skaffa licenser för nytt innehåll.

1. Klienten tolkar det skyddade innehållet när det börjar laddas ned eller direktuppspelas på konsumentens dator och extraherar URL:en för återförsäljarens licensserver från de DRM-metadata som är inbäddade i filen.

   DRM-metadata är vanligtvis separata från innehållet, t.ex. inbäddade i en medföljande manifestfil eller som binära blob, men kan också bäddas in i innehållsfilen. Klienten kontaktar licensservern på den angivna URL:en och skaffar en licens (som beskrivs nedan i steg 4).
1. Kunden köper en licens från återförsäljarens licensserver.

   Vid hämtning av licenser skickar klienten information som identifierar det begärda innehållet ( *DRM-metadata*) och datorcertifikatet (som identifierar konsumentens dator) till återförsäljarens licensserver. Licensbegäran som skickas till servern krypteras med den publika transportnyckeln, som också ingår i DRM-metadata.

   Licensservern - som kan integreras i återförsäljarens infrastruktur för fakturering och autentisering - kan utföra en kontroll av affärsregler för att verifiera att användaren har behörighet att visa det begärda innehållet. Om affärsreglerna tillåter det utfärdar licensservern en licens som innehåller innehållskrypteringsnyckeln för att dekryptera innehållet och de användningsregler som är kopplade till användarens konto. Licensservern dekrypterar begäran med den privata nyckeln Transport för att bearbeta en licensbegäran. CEK:n i metadata dekrypteras med den privata nyckeln för licensservern och omkrypteras för att binda licensen till den enhet som gjorde begäran. Licensen signeras med licensserverns privata nyckel. Licenssvaret signeras med den privata transportnyckeln och krypteras innan det returneras till klienten.

   Om licensen tillåter det lagrar klienten licensen så att *offlineåtkomst* till licensen. Med cachning av licenser kan konsumenten visa skyddat innehåll utan att behöva skaffa om en licens varje gång de vill visa innehållet.

1. När Flashen Player eller Adobe AIR runtime-klienten har en licens extraherar klienten CEK från licensen och konsumenten kan se det innehåll som han/hon har behörighet att komma åt.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   I föregående exempel visas bara ett möjligt arbetsflöde. Du kan också använda ett arbetsflöde med en proaktiv nedladdning av innehåll där licensköpet sker mycket senare. Ett annat alternativ är att implementera ett förbeställningsarbetsflöde där licensköpet sker innan innehållet öppnas.
