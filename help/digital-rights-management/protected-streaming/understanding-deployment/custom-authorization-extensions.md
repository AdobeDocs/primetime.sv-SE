---
description: Du kan anropa anpassad auktoriseringslogik under licensköp för att bestämma om en licens ska utfärdas till den begärande klienten.
seo-description: Du kan anropa anpassad auktoriseringslogik under licensköp för att bestämma om en licens ska utfärdas till den begärande klienten.
seo-title: Anpassade auktoriseringstillägg
title: Anpassade auktoriseringstillägg
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Anpassade auktoriseringstillägg{#custom-authorization-extensions}

Du kan anropa anpassad auktoriseringslogik under licensköp för att bestämma om en licens ska utfärdas till den begärande klienten.

Om du vill implementera ett eget tillägg för kundauktorisering måste du först ta en titt på exempelkoden som finns i exempelkatalogen. [!DNL SampleAuthorizer.java] Den kompilerade versionen av det här exemplet finns i [!DNL flashaccess-license-server-ext-sample.jar].

Om du vill skapa ett eget tillägg måste du implementera `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` gränssnittet och se till att [!DNL flashaccess-license-server-exts.jar] och [!DNL commons-logging.jar] finns i byggsökvägen ( [!DNL adobe-flashaccess-sdk.jar] måste också finnas i byggsökvägen om du använder vissa fält i `IMessageFacade`).

Om du vill distribuera tillägget måste du kopiera burk- eller klassfilerna till *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Om du vill uppdatera burk- eller klassfilerna måste du starta om servern innan den uppdaterade versionen kan användas. Du måste också lägga till namnet på klassen Author i klientkonfigurationsfilen.
