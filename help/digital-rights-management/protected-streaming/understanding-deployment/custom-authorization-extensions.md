---
description: Du kan anropa anpassad auktoriseringslogik under licensköp för att bestämma om en licens ska utfärdas till den begärande klienten.
title: Anpassade auktoriseringstillägg
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Anpassade auktoriseringstillägg{#custom-authorization-extensions}

Du kan anropa anpassad auktoriseringslogik under licensköp för att bestämma om en licens ska utfärdas till den begärande klienten.

Om du vill implementera ett eget tillägg för kundauktorisering måste du först ta en titt på exempelkoden [!DNL SampleAuthorizer.java] som finns i exempelkatalogen. Den kompilerade versionen av det här exemplet finns i [!DNL flashaccess-license-server-ext-sample.jar].

Om du vill skapa ett eget tillägg måste du implementera gränssnittet `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` och se till att [!DNL flashaccess-license-server-exts.jar] och [!DNL commons-logging.jar] finns i byggsökvägen ( [!DNL adobe-flashaccess-sdk.jar] måste också finnas i byggsökvägen om du använder vissa fält i `IMessageFacade`).

Om du vill distribuera tillägget måste du kopiera jar- eller klassfilerna till *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Om du vill uppdatera burk- eller klassfilerna måste du starta om servern innan den uppdaterade versionen kan användas. Du måste också lägga till namnet på klassen Author i klientkonfigurationsfilen.
