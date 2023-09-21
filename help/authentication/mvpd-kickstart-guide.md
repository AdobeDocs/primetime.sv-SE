---
title: Integrationsplan för MVPD
description: Integrationsplan för MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# MVPD-startguide: MVPD-direktintegreringsplan {#mvpd-dir-int-plan}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#mvpd-kickstart-intro}

Välkommen till Adobe Primetime-autentisering för TV Everywhere.  Vi ser fram emot att få samarbeta med dig.

>[!NOTE]
>
>Det här är Kickstart-guiden för distributörer av flerkanalsvideo (MVPD). Om du är programmerare (innehållsleverantör), se [Programmerarnas Kickstart Guide](/help/authentication/programmer-kickstart-guide.md).

Support är alltid tillgänglig genom Primetimes biljettsystem för autentisering på Zendesk. Här hittar du också exempel, dokumentation och videokurser för våra processer. För att kunna använda [Zendesk](https://adobeprimetime.zendesk.com/)måste du registrera dig och skapa ett konto på https://tve.zendesk.com/home. Det finns ingen gräns för hur många användare du kan registrera och vem som kan se eller posta kommentarer på en arkiverad biljett. Alla supportfrågor kan ställas till: tve support på adobe.com

**Teamkontakter**:

**Support** - För alla frågor, incidenter eller förslag på nya funktioner **tve-support@adobe.com**.

## 1. Snabbmöten {#kickoff-meetings}

Omfattningen av dessa möten är inledandet av tekniska diskussioner mellan Adobe och det fleråriga utvecklingsprogrammet. I det här skedet av processen måste dokumentation delas från båda sidor. Som en uppföljning måste Adobe öppna en biljett i vårt biljettsystem (https://tve.zendesk.com/) för att spåra integreringens status.

## 2. Funktioner {#features}

Adobe kommer att upprätta ett statussamtal varje vecka för att diskutera och följa upp det övergripande schemat, stegen, tidslinjen och implementeringsinformationen för integreringen. I den här fasen gör Adobe en översyn av specifikationerna för det virtuella dokumentationsdokumentet. Resultatet av detta bör vara en specifikationssida som beskriver alla funktioner som krävs av det mobila dokumentationsdokumentet. MVPD skickar ett specifikationsdokument till Adobe med information om MVPD:s autentisering-/auktoriseringsimplementering.

Objekt som ska klargöras, se [MVPD-integreringsfunktioner](/help/authentication/mvpd-integr-features.md).

Det finns flera inställningar som behöver beskrivas i detalj:

* **MVPD:s logotyp URL** - Det här är en fil med följande dimensioner: 112 x 33 pixlar. Logotypen visas av programmerare på deras webbplatser när användaren klickar på knappen &quot;Logga in&quot; för att välja sin Pay TV-leverantör.
* **TTL-värden (time to live)** - TTL anges vanligtvis av MVPD under autentiserings-/auktoriseringsprocessen. Adobe kan dock åsidosätta dessa TTL-värden och ange olika värden beroende på vad som överenskommits av både Programmer och MVPD.
* **Visningsnamn** - Detta visas av programmerare på deras webbplatser när användaren klickar på knappen &quot;Logga in&quot; för att välja sin Pay TV-leverantör.
* **Testa autentiseringsuppgifter** - Båda profilerna (staging och production) bör ha en lista med testautentiseringsuppgifter.

>[!IMPORTANT]
>
>Varje gång en användare initierar ett tillståndsflöde kopplas han/hon till ett enda ogenomskinligt, unikt användar-ID.  Användar-ID:t används för att identifiera användaren av en programmerarapp, men härstammar från MVPD.

>[!CAUTION]
>
>Ett viktigt meddelande för varje MVPD: användar-ID:t får INTE innehålla någon PII (Personally Identiitable Information), information som kan användas fristående eller tillsammans med annan information för att identifiera, kontakta eller hitta användaren.

## 2. Utbyte av metadata {#metadata-ex}

De två sidorna måste utbyta metadata för alla berörda miljöer (produktion, mellanlagring osv.).

* **Adobe**
   * För testmiljön kan AdobeSP-metadata hämtas från: [Sp-metadata för autentiseringsmellanlagring](https://sp.auth-staging.adobe.com/sp/metadata)
   * För produktionsmiljön kan AdobeSP-metadata hämtas från: [Sp-metadata för autentiseringsproduktion](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * Lägga till metadata (mellanlagring/produktion).

## 4. Tillåt IP-lista {#allow-ip-list}

Följande IP-adresser ska vitlistas i MVPD:s brandvägg. Kontakta Adobe för att få en lista över IP-adresser.

* Primetime-autentisering kräver att brandväggar öppnas på portarna 80 och 443 för att tillåta åtkomst till begränsade resurser.

* MVPD måste lägga till en lista med IP-adresser för autentiserings- och auktoriseringsservrar (om så är fallet).

## 5. Utveckling {#deve}

Utvecklingsfasens varaktighet bestäms efter att specifikationerna har granskats och med beaktande av de punkter som de båda sidorna signerar. Adobe måste skriva anpassad kod för auktoriseringsdelen.

>[!NOTE]
>
>Observera att auktorisering utförs per resurs. Auktoriseringstransaktionen utförs vanligtvis med en ID-sträng som skickas från Programmerarens webbplats och som representerar den kanal som användaren begär auktorisering för. Detta resurs-ID är upprättat mellan Programmer och MVPD och kan vara så detaljerat som nödvändigt.

## 6. Adobe-miljöer {#adobe-env}

Adobe erbjuder olika miljöer för olika faser av utvecklingsprocessen:

* **Prekvalificering** (PRE-QUAL): I PRE-QUAL-miljön finns nästa release-kandidat. Adobe integrerar till att börja med nya partners i den här miljön innan man uppgraderar integreringen till releasemiljön. Partners har två veckor på sig att testa PRE-QUAL-miljön och måste uttryckligen begära ändringar i PRE-QUAL-konfigurationen (kontakta Adobe för mer information om ändringsförfrågningsprocessen). Felkorrigeringar utlöser nya distributioner i den här miljön.
* **Frigör** (RELEASE): Adobe nuvarande produktionsbygge distribueras till en aktiv miljö här.

Mer information om hur du använder Adobe-miljöer finns i [Förstå Adobe-miljöer](/help/authentication/understanding-the-adobe-environments.md)

## 7. Mellanlagringsdistribution {#stag-env}

Baserat på de metadata som tagits emot från MVPD kommer Adobe att skapa och konfigurera ett nytt MVPD i autentiseringssystemet Primetime. Detta distribueras i Adobe prequal staging-miljö och konfigureras med vår testprogrammerare (TestDistributors).

MVPD måste göra samma distribution i QA-/staging-/testmiljön.

## 8. Testa och felsöka {#tes-troubleshoot}

I den här fasen testar och felsöker Adobe och MVPD integreringen. Primetimes autentiseringsteam kan testa integreringen med hjälp av Adobe API-testwebbplatsen. Mer information om hur du använder Adobe PPAPI-testwebbplatsen finns på [Testa autentiserings- och auktoriseringsflöden med Adobe API-testwebbplats](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

När testningen och felsökningen är slutförd aktiveras integreringen i testmiljön i Adobe. Nu kan Adobe integrera MVPD med en riktig programmerare.

## 9. Produktionsdistribution {#prod-dep}

* MVPD måste distribueras först i produktionsprofilen för att kunna testa anslutningen.

* Adobe driftsätter i förproduktion.

* Alla parter kan nu testa i produktionsprofilen.

* Om allt är bra nu kan Adobe flytta integreringen till produktionsmiljön (&quot;live&quot;) som är tillgänglig för alla användare.

## 10. Eskaleringsprocedurer {#esc-proc}

När integreringen är klar i produktionen är det avgörande att kunna erbjuda den bästa kundupplevelsen. För att säkerställa bästa möjliga svar i händelse av problem med serverdriftstopp, måste de mobila skyddsprofilerna tillhandahålla dokumentation om eskaleringsproceduren för problem som Adobe uppmärksammas på.

Adobe tillhandahåller i sin tur distributörer av videoprogrammeringstjänster med den senaste eskaleringsprocessen för autentisering i Primetime.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
