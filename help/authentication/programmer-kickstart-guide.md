---
title: Programmeraren kickstart
description: Programmeraren kickstart
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Programmeraren kickstart {#programmer-kickstart-guide}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#prog-kickstart-guide-intro}

Välkommen till Adobe Primetime-autentisering för TV Everywhere. Vi ser fram emot att få samarbeta med dig.

>[!NOTE]
>
>Detta är Kickstart Guide for Programmers (innehållsleverantörer). Om du har en distributör av flerkanalsvideo Programming (MVPD), se [MVPD - startguide](/help/authentication/mvpd-kickstart-guide.md).


Kontakter för Adobe Primetime-autentisering:

* Support - för alla frågor, incidenter eller förslag på nya funktioner, `tve-support@adobe.com`
* En aktiveringskontakt tilldelas ditt projekt när projektet startar.

I följande information beskrivs några viktiga första steg för att komma vidare till en stabil och effektiv start. Målet är att ge en förklaring och förväntan om hur vi kommer att samarbeta med partners för att uppnå integreringar. Observera avsnitten &quot;du kommer att ange&quot; / &quot;Adobe kommer att tillhandahålla&quot; nedan för varje objekt. De listas som en checklista eller guide när vi arbetar med projektet.

I det här dokumentet förutsätts att programmerare är registrerade att arbeta med en vald MVPD-partner.

## Frigör schema {#release-schedule}

Utvecklingscykeln för Adobe-sprint är planerad så att du kan se när våra releaser är schemalagda och hur varje release främjas via vårt utvecklingssystem.

När varje utskrift är klar är den tillgänglig för QE, eller för att se nya implementeringar på vår UAT-server.

Ungefär var sjätte vecka kommer en release att göras till Adobe prekvalificeringsservern. (Det här är servern där vi håller den föreslagna nästa version medan vi genomför en slutlig QE.) De här byggnaderna innehåller allt arbete som utförts i sprints sedan den senaste släppningen. För närvarande finns det ett QE-fönster på två veckor där partners kan testa den här versionen.

Om inga kritiska problem uppstår under det föregående två veckor långa testfönstret kommer releasen att höjas till liveproduktion. Det innebär att integreringen kommer att vara tillgänglig i Adobe Release-miljön, men våra partners väljer när de ska offentliggöra releasen.

<!--For the latest release schedule information, see the Release Calendar.-->

## Supportdokumentation {#supp-doc}

Adobe kommer att tillhandahålla

* Distributionshandbok: **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* Tillgång till vårt Zendesk-system för kundsupport. Här hittar du också exempel, information och videokurser om några av processerna. För att få tillgång till det här dokumentet på Zendesk, tillsammans med andra dokument som publicerats där, måste du registrera dig och skapa ett konto på `https://tve.zendesk.com/home`. Det finns ingen gräns för hur många användare du kan registrera.  Du kan se och dela kommentarer på alla arkiverade biljetter. Alla supportfrågor ska ställas till `tve-support@adobe.com`.
* [Integreringshandbok för programmerare](/help/authentication/programmer-integration-guide-overview.md)
* Verifieringsbibliotek för medietoken: `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## Konfigurera testmiljö {#test-env-setup}

Adobe ska först ställa in dig på testplatsen Adobe, där Adobe fungerar som ett sidoskydd för teständamål. Teamet kan sedan skapa en testwebbplats som anropar Adobe API:t. Använd MVPD-standardväljaren och välj Adobe som idP.

Du kommer att ange:

1. Begärande-ID. Detta är en sträng som unikt identifierar varumärket på webbplatsen eller det program som begär Adobe Primetime-autentisering. Själva strängen är godtycklig men måste avtalas mellan Adobe och programmeraren
1. Kanalinformation. Detta är en uppsättning strängar som identifierar innehållskanaler som begärande-ID begär. I många fall är kanalen och begärande-ID desamma. Du kan dock ha flera kanaler med innehåll som kan begäras av samma ID. Kanalnamnssträngarna ska motsvara kabel-TV-kanalerna. Vissa MVPD-program validerar det här värdet via AuthN- och/eller AuthZ-protokollet.
1. Domännamn (tillåts för det begärande-ID:t). Detta är en lista över faktiska domännamn som Adobe kommer att visa för att godkänna begärande-ID. Detta garanterar att endast godkända domäner har tillgång till Adobe Primetime-autentisering med dina metadata. Obs! Domännamn som är giltiga för produktion kan vara olika för testning/testning och både ska anges och identifieras.

Adobe kommer att upprätta kontot och Adobe kommer att tillhandahålla följande:

* Inloggning och lösenord för att komma åt testwebbplatsen

## Konfigurera med MVPD {#setup-mvpd}

I det här avsnittet beskrivs vad du behöver när du migrerar från testwebbplatsen i Adobe för att arbeta med ett PDF-dokument.

Du kommer att tillhandahålla (via MVPD):

* **Två uppsättningar autentiseringsuppgifter**:
   * AuthN + AuthZ : inloggning/lösenord för en användare som är autentiserad och auktoriserad
   * AuthN + Non-AuthZ: inloggning/lösenord för en användare som är autentiserad men inte auktoriserad
* **Resurs-ID**. Detta är en specifik innehållsidentifierare som valideras med ett MVPD-protokoll över AuthZ-protokollet. Detta kan vara på kanal-, show-, avsnitt- eller tillgångsnivå; det ska överenskommas med ditt MVPD.

Adobe Primetime-autentisering stöder ett MRSS-baserat metadatamatchema, vilket innebär att resurs-ID:n kan vara så specifika som behövs, och kan innehålla identifierare som kan vara unika för ett specifikt MVPD.

**NYTT Integrering med MVPD**: Det är viktigt att komma ihåg att ditt valda MVPD spelar en viktig roll när det gäller att slutföra integreringen. Adobe måste skriva kod för varje MVPD enligt sina specifikationer. Innan dessa steg är slutförda kan du inte välja det MVPD-programmet i dialogrutan eller slutföra produkttestningen. Adobe måste schemalägga detta arbete i förväg för att passa nästa tillgängliga sprint. (Aktuell schemainformation finns i Release Calendar.)

**Befintliga MVPD-integreringar**: Om ditt MVPD-program redan är konfigurerat med Adobe bör anslutningsstegen vara mycket enklare (snabbare) och anslutningen kan ofta göras med hjälp av konfigurationsändringar.

>[!NOTE]
>
>MVPD måste FORTFARANDE aktivera Programmeraren och teckna avtal.

**QE med MVPD**: Alla integreringar innefattar gemensamma QE, och eftersom slutanvändaren i slutändan är kund hos MVPD har många testcykler innan man trycker&quot;live&quot;. Eftersom detta innebär schemaläggning av MVPD-resurser kan detta försenas.

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->
