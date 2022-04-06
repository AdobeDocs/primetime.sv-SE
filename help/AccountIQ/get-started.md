---
title: Kontots IQ kommer igång med kontots IQ, krav och introduktion
description: 'Anlita kunder, förutsättningar och komma igång med kontots IQ. '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Så här kommer du igång med kontots IQ {#onboarding}

Läs vidare för att få information om förutsättningarna för att använda konto-IQ och hur kan ert företag komma igång med att titta närmare på poängen för kontodelning för prenumeranter.

## Förutsättningar {#prerequisites}

* Organisationen måste vara registrerad i [!DNL Adobe Marketing Cloud] organisationer.

* Användare i den organisationen bör tilldelas skrivskyddad TVE Dashboard eller TVE Dashboard.

### Krav för webbläsare {#browser-prerequisites}

Konto-IQ är en webbtjänst. Den är kompatibel med den senaste versionen av följande webbläsare:

* Google Chrome
* Mozilla Firefox
* Safari-version

### Hur skaffar man in organisationer på konto-IQ? {#steps-to-onboard}


Det här är vad vi har för tillfället. Planen är att ta bort dma_primetime-kontrollen och ha en dedikerad profil för AIQ. De användare som behöver ha åtkomst till konsolen behöver den användarprofilen. Detta är dock inte implementerat just nu.

1. Om du har deras organisation ombord på Adobe Marketing Cloud @Eric eller @Peter kan du ta det här.  Jag tror att det nu heter&quot;Experience Cloud&quot;, men det är inte mycket.  Finns det fler detaljer i detta? Hanteras detta av en annan grupp? Om så är fallet, tillhandahåller vi en länk, kontakt osv.? Detta bör även innehålla en kavaat om att kontrollera om deras organisation redan är en del av Experience Cloud.

2. Med skrivskyddade TVE Dashboard-profiler för TVE Dashboard som är tilldelade användare i http://adminconsole.adobe.com/.
@Eric, vet du hur man gör det här?  Finns det understeg?  Kan vi förklara för kunderna varför de valt Skrivskyddad eller Skrivskyddad?
@Cristina, kan du ge en kort förklaring till att detta är ett tillfälligt tillvägagångssätt och kanske hur det kommer att fungera i nästa version?

3. Får deras organisation vitlistad på AIQ-sidan @Cristina, finns det någon process som vi kan införa för att hantera detta?  Skicka t.ex. ett e-postmeddelande till&quot;DL-AdobePass-Eng AdobePass-Eng@adobe.com&quot; med organisationens organisations-ID, etc.

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

När du öppnar Adobe Enterprise Dashboard ser du de två nya användargrupperna i din Adobe Marketing Cloud-organisation:

Skrivskyddad TVE Dashboard - medlemmarna i den här gruppen har fullständig behörighet för alla redigerbara avsnitt i instrumentpanelens TVE Dashboard Skrivskyddad - medlemmarna i den här gruppen har bara visningsrättigheter för hela instrumentpanelen Lägg till ditt konto i användargruppen Skrivskyddad för TVE Dashboard, i Adobe Enterprise Dashboard, och logga sedan in i Adobe Primetime TVE Dashboard.  Efteråt kan du hantera användarbehörigheter i Adobe Enterprise Dashboard genom att lägga till och ta bort användare i de två användargrupper som listas ovan.

...........

I den dokumentation som du angav finns det en del som heter&quot;Komma igång med användaretableringen för Primetime TVE Dashboard&quot; som gäller för Adobe Pass-konsolen, men som även ska likna för AIQ.
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide Organisationen som är intresserad av AIQ bör vara en organisation som är registrerad i Adobe Marketing Cloud Orgs. Användare i den organisationen bör tilldelas skrivskyddad TVE Dashboard eller TVE Dashboard.
Dessa användargrupper anger produktkontexten dma_primetime för användarkontona, endast om du är medveten om det. I AIQ-koden söker vi efter den här produktkontexten när vi ger åtkomst. Internt har vi ett villkor i koden: Org-id:t bör vitlistas för att användarna ska få tillgång till sina data.
Det här är vad vi har för tillfället. Planen är att ta bort dma_primetime-kontrollen och ha en dedikerad profil för AIQ. De användare som behöver ha åtkomst till konsolen behöver den användarprofilen. Detta är dock inte implementerat just nu.

..........................

1. Anta att de är anställda i Adobe Marketing Cloud
2. Med skrivskyddade TVE Dashboard-profiler för TVE Dashboard som är tilldelade användare i http://adminconsole.adobe.com/.
3. Anta att deras organisation är vitlistad på AIQ-sidan
