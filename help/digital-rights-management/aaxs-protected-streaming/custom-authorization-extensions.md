---
title: Anpassade auktoriseringstillägg
description: Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Anpassade auktoriseringstillägg {#custom-authorization-extensions}

Anpassad auktoriseringslogik kan anropas under licensköp för att avgöra om en licens ska utfärdas till den begärande kunden.

Om du vill implementera ett eget tillägg för kundauktorisering ska du först titta på [!DNL SampleAuthorizer.java] exempelkod i exempelkatalogen (den kompilerade versionen av det här exemplet finns i flashaccess-license-server-ext-sample.jar).

Implementera `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` och se till att `flashaccess-license-server-exts.jar` och `commons-logging.jar` finns på byggsökvägen `adobe-flashaccess-sdk.jar` måste också finnas på byggsökvägen om du använder vissa fält i `IMessageFacade`). Om du vill distribuera tillägget kopierar du behållar- eller klassfilerna till *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Om du behöver uppdatera jar- eller klassfilerna måste servern startas om innan den uppdaterade versionen används. Du måste också lägga till namnet på klassen Author i klientkonfigurationsfilen.
