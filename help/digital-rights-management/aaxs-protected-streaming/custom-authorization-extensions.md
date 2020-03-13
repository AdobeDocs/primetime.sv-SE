---
seo-title: Anpassade auktoriseringstillägg
title: Anpassade auktoriseringstillägg
description: Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.
seo-description: Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0

---


# Anpassade auktoriseringstillägg {#custom-authorization-extensions}

Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.

För att implementera ett eget tillägg för kundauktorisering ska du först titta på exempelkoden som finns i exempelkatalogen (den kompilerade versionen av det här exemplet finns i flashaccess-license-server-ext-sample.jar). [!DNL SampleAuthorizer.java]

Om du vill skapa ett eget tillägg implementerar du `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` gränssnittet och ser till att `flashaccess-license-server-exts.jar` och `commons-logging.jar` finns på byggsökvägen `adobe-flashaccess-sdk.jar` måste också finnas på byggsökvägen om du använder vissa fält i `IMessageFacade`). Om du vill distribuera tillägget kopierar du dina jar- eller klassfiler till *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Om du behöver uppdatera jar- eller klassfilerna måste servern startas om innan den uppdaterade versionen används. Du måste också lägga till namnet på klassen Author i klientkonfigurationsfilen.
