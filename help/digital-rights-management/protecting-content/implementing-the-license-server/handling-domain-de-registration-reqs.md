---
title: Hantera begäranden om domänavregistrering
description: Hantera begäranden om domänavregistrering
copied-description: true
exl-id: 14b97ba2-9344-4d84-8c52-f33126337454
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Hantera begäranden om domänavregistrering {#handle-domain-de-registration-requests}

Om klientprogrammet måste lämna en domän, anropas `DRMManager.removeFromDeviceGroup()`ActionScript API eller `leaveLicenseDomain()` iOS API för att initiera domänavregistreringsprocessen. Avregistrering av domäner är en tvåstegsprocess. Klienten skickar först en förhandsgranskningsbegäran om avregistrering. Domänservern undersöker begäran och avgör om klienten får lämna domänen. Ett fel kan returneras om datorn inte är en del av domänen. När svaret är klart tar klienten bort domänens autentiseringsuppgifter och alla licenser som har utfärdats till den domänen. Sedan skickas en avregistreringsbegäran.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;Domänserver-URL i metadata: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. I annat fall är begärande-URL:en Domänserver-URL i metadata&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

Vid bearbetning av begäran om domänavregistrering använder servern `getRequestPhase()` för att avgöra om kunden befinner sig i förhandsgransknings- eller avregistreringsfasen. I förhandsgranskningsfasen undersöker domänservern begäran och avgör om klienten får lämna domänen eftersom begäran kan nekas. Begäran kan till exempel nekas om datorn inte är en del av domänen. I avregistreringsfasen registrerar servern det faktum att datorn har lämnat domänen. Vi rekommenderar att servern utvärderar samma logik i förhandsgranskningsbegäran som i den faktiska avregistreringsbegäran för att minimera risken för att den andra fasen misslyckas.
