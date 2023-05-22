---
title: Återkallar datorautentiseringsuppgifter
description: Återkallar datorautentiseringsuppgifter
copied-description: true
exl-id: 6dffcb1f-3e9b-423c-800a-90075afe779b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Återkallar datorautentiseringsuppgifter{#revoking-machine-credentials}

Adobe har en lista över återkallade certifikat för att återkalla datorautentiseringsuppgifter som är kända att vara komprometterade. Denna lista över återkallade certifikat används automatiskt av SDK. Om det finns ytterligare datorer som du inte vill att din licensserver ska utfärda licenser till, kan du skapa en lista över återkallade datorer och lägga till utfärdarens namn och serienummer för de maskintoken som du vill utesluta (använd `MachineToken.getMachineTokenId()` för att hämta utfärdarens namn och serienummer för datorcertifikatet).

När du återkallar datorautentiseringsuppgifter används en `RevocationListFactory` -objekt. Så här skapar du en lista över återkallade certifikat, läser in en befintlig lista över återkallade certifikat och kontrollerar om en maskintoken har återkallats med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i [Konfigurera utvecklingsmiljön](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) i ditt projekt.
1. Skapa en `ServerCredentialFactory` -instans för att läsa in de autentiseringsuppgifter som krävs för signering. Autentiseringsuppgifterna för licensservern används för att signera listan över återkallade certifikat.
1. Skapa en `RevocationListFactory` -instans.
1. Ange utfärdare och serienummer för den datortoken som ska återkallas med en `IssuerAndSerialNumber` -objekt. Alla Adobe Access-begäranden innehåller en maskintoken.
1. Skapa en `RevocationList` objekt med `IssuerAndSerialNumber` objekt som du just har skapat och lagt till det i spärrlistan genom att skicka det till `RevocationListFactory.addRevocationEntry()`. Generera den nya spärrlistan genom att ringa `RevocationListFactory.generateRevocationList()`.
1. Om du vill spara återkallningslistan kan du serialisera den genom att anropa `RevocationList.getBytes()`. Om du vill läsa in listan ringer du `RevocationListFactory.loadRevocationList()` och skicka i den serialiserade listan.
1. Kontrollera att signaturen är giltig och att listan signerades av rätt licensserver genom att ringa `RevocationList.verifySignature()`.
1. Om du vill kontrollera om en post har återkallats skickar du `IssuerAndSerialNumber` objekt till `RevocationList.isRevoked()`. Återkallningslistan kan också skickas till `HandlerConfiguration` om du vill att SDK ska tillämpa återkallningslistan för alla autentiserings- och licensbegäranden.

Lägga till fler poster i en befintlig `RevocationList`, läser in en befintlig återkallningslista. Skapa ett nytt `RevocationListFactory` och se till att öka CRL-numret. Utlysning `RevocationListFactioryEntries.addRevocationEntries` om du vill lägga till alla poster från den gamla listan i den nya listan. Utlysning `RevocationListFactory.addRevocationEntry` om du vill lägga till nya spärrposter i RevocationList.

Exempelkod som visar hur du skapar en återkallningslista, läser in en befintlig återkallningslista och kontrollerar om en maskintoken har återkallats finns i `com.adobe.flashaccess.samples.revocation.CreateRevocationList` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.
