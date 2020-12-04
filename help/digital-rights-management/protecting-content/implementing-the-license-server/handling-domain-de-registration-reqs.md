---
seo-title: Hantera begäranden om domänavregistrering
title: Hantera begäranden om domänavregistrering
uuid: 80dbbb60-9005-4a3d-86bf-26cdbed86452
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Hantera begäran om domänavregistrering {#handle-domain-de-registration-requests}

Om klientprogrammet måste lämna en domän anropar det API:t `DRMManager.removeFromDeviceGroup()`ActionScript eller iOS-API:t `leaveLicenseDomain()` för att initiera domänavregistreringsprocessen. Avregistrering av domäner är en tvåstegsprocess. Klienten skickar först en förhandsgranskningsbegäran om avregistrering. Domänservern undersöker begäran och avgör om klienten får lämna domänen. Ett fel kan returneras om datorn inte är en del av domänen. När svaret är klart tar klienten bort domänens autentiseringsuppgifter och alla licenser som har utfärdats till den domänen. Sedan skickas en avregistreringsbegäran.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;Domänserver-URL i metadata: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. I annat fall är begärande-URL:en Domänserverns URL i metadata + &quot; [!DNL /flashaccess/dereg/v3]&quot;

När servern bearbetar begäran om domänavregistrering använder den `getRequestPhase()` för att avgöra om klienten befinner sig i förhandsgransknings- eller avregistreringsfasen. I förhandsgranskningsfasen undersöker domänservern begäran och avgör om klienten får lämna domänen eftersom begäran kan nekas. Begäran kan till exempel nekas om datorn inte är en del av domänen. I avregistreringsfasen registrerar servern det faktum att datorn har lämnat domänen. Vi rekommenderar att servern utvärderar samma logik i förhandsgranskningsbegäran som i den faktiska avregistreringsbegäran för att minimera risken för att den andra fasen misslyckas.
