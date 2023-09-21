---
title: Hantera begäranden om domänavregistrering
description: Hantera begäranden om domänavregistrering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Hantera begäranden om domänavregistrering{#handling-domain-de-registration-requests}

Om klientprogrammet måste lämna en domän, anropas `DRMManager.removeFromDeviceGroup()`ActionScript-API eller `leaveLicenseDomain()` iOS API för att initiera domänavregistreringsprocessen. Avregistrering av domäner är en tvåstegsprocess. Klienten skickar först en förhandsgranskningsbegäran om avregistrering. Domänservern undersöker begäran och avgör om klienten får lämna domänen (ett fel kan returneras om datorn inte är en del av domänen). När svaret är klart tar klienten bort sina domänreferenser och alla licenser som utfärdats till den domänen och skickar sedan en avregistreringsbegäran.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Om både klienten och servern stöder protokoll version 5 är förfrågnings-URL:en &quot;Domänserver-URL i metadata: + &quot;/flashaccess/dereg/v4&quot;. I annat fall är begärande-URL:en Domänserver-URL i metadata&quot; + &quot;/flashaccess/dereg/v3&quot;

Vid bearbetning av begäran om domänavregistrering använder servern `getRequestPhase()` för att avgöra om kunden befinner sig i förhandsgransknings- eller avregistreringsfasen. I förhandsgranskningsfasen undersöker domänservern begäran och avgör om klienten får lämna domänen (begäran kan till exempel nekas om datorn inte är en del av domänen). I avregistreringsfasen registrerar servern det faktum att datorn har lämnat domänen. Vi rekommenderar att servern utvärderar samma logik i förhandsgranskningsbegäran som i den faktiska avregistreringsbegäran för att minimera risken för att den andra fasen misslyckas.
