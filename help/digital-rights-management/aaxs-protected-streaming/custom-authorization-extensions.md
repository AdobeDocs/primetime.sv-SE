---
title: Anpassade auktoriseringstillägg
description: Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Anpassade auktoriseringstillägg {#custom-authorization-extensions}

Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.

Om du vill implementera ett eget tillägg för kundauktorisering ska du först titta på exempelkoden i exempelkatalogen (den kompilerade versionen av det här exemplet finns i flashaccess-license-server-ext-sample.jar).[!DNL SampleAuthorizer.java]

Om du vill skapa ett eget tillägg implementerar du gränssnittet `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` och ser till att `flashaccess-license-server-exts.jar` och `commons-logging.jar` finns på byggsökvägen `adobe-flashaccess-sdk.jar` måste också finnas på byggsökvägen om du använder vissa fält i `IMessageFacade`). Om du vill distribuera tillägget kopierar du dina jar- eller klassfiler till *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Om du behöver uppdatera jar- eller klassfilerna måste servern startas om innan den uppdaterade versionen används. Du måste också lägga till namnet på klassen Author i klientkonfigurationsfilen.
