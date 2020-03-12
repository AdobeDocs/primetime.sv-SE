---
seo-title: Hantera begäranden om domänavregistrering
title: Hantera begäranden om domänavregistrering
uuid: 6f056b2b-374d-4e4d-926a-68605b2c923b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Hantera begäranden om domänavregistrering{#handling-domain-de-registration-requests}

Om klientprogrammet måste lämna en domän anropar det `DRMManager.removeFromDeviceGroup()`ActionScript-API:t eller `leaveLicenseDomain()` iOS-API:t för att initiera domänavregistreringsprocessen. Avregistrering av domäner är en tvåstegsprocess. Klienten skickar först en förhandsgranskningsbegäran om avregistrering. Domänservern undersöker begäran och avgör om klienten får lämna domänen (ett fel kan returneras om datorn inte är en del av domänen). När svaret är klart tar klienten bort sina domänreferenser och alla licenser som utfärdats till den domänen och skickar sedan en avregistreringsbegäran.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;Domänserver-URL i metadata: + &quot;/flashaccess/dereg/v4&quot;. I annat fall är begärande-URL:en Domänserver-URL i metadata&quot; + &quot;/flashaccess/dereg/v3&quot;

När servern bearbetar begäran om domänavregistrering använder den `getRequestPhase()` för att avgöra om klienten befinner sig i förhandsgransknings- eller avregistreringsfasen. I förhandsgranskningsfasen undersöker domänservern begäran och avgör om klienten får lämna domänen (begäran kan till exempel nekas om datorn inte är en del av domänen). I avregistreringsfasen registrerar servern det faktum att datorn har lämnat domänen. Vi rekommenderar att servern utvärderar samma logik i förhandsgranskningsbegäran som i den faktiska avregistreringsbegäran för att minimera risken för att den andra fasen misslyckas.
