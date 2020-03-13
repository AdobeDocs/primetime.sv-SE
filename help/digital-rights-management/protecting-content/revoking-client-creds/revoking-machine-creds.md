---
seo-title: Återkallar datorautentiseringsuppgifter
title: Återkallar datorautentiseringsuppgifter
uuid: 3647c843-5f1a-457e-949d-10a6278b1c29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Återkallar datorautentiseringsuppgifter {#revoking-machine-credentials}

Adobe har en lista över återkallade certifikat för återkallade datorreferenser som man vet är komprometterade. Denna CRL används automatiskt av SDK. Om det finns ytterligare datorer som du inte vill att din licensserver ska utfärda licenser till, kan du skapa en lista över återkallade datorer och lägga till utfärdarens namn och serienummer för de maskintoken som du vill utesluta (använd `MachineToken.getMachineTokenId()` för att hämta utfärdarens namn och serienummer för datorcertifikatet).

När du återkallar datorautentiseringsuppgifter används ett `RevocationListFactory` objekt. Så här skapar du en lista över återkallade certifikat, läser in en befintlig lista över återkallade certifikat och kontrollerar om en maskintoken har återkallats med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i [Konfigurera utvecklingsmiljön](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) i ditt projekt.
1. Skapa en `ServerCredentialFactory` instans för att läsa in de autentiseringsuppgifter som krävs för signering. Autentiseringsuppgifterna för licensservern används för att signera listan över återkallade certifikat.
1. Skapa en `RevocationListFactory` instans.
1. Ange utfärdare och serienummer för den datortoken som ska återkallas med ett `IssuerAndSerialNumber` objekt. Alla DRM-begäranden från Adobe Primetime innehåller en maskintoken.
1. Skapa ett `RevocationList` objekt med det `IssuerAndSerialNumber` objekt du just skapade och lägg till det i listan över spärrningar genom att skicka det till `RevocationListFactory.addRevocationEntry()`. Generera den nya spärrlistan genom att ringa `RevocationListFactory.generateRevocationList()`.

1. Om du vill spara återkallningslistan kan du serialisera den genom att anropa `RevocationList.getBytes()`. Om du vill läsa in listan anropar du `RevocationListFactory.loadRevocationList()` och skickar den serialiserade listan.

1. Kontrollera att signaturen är giltig och att listan signerades av rätt licensserver genom att ringa `RevocationList.verifySignature()`.
1. Om du vill kontrollera om en post har återkallats skickar du objektet till `IssuerAndSerialNumber` `RevocationList.isRevoked()`. Återkallningslistan kan också skickas `HandlerConfiguration` till så att SDK framtvingar återkallningslistan för alla autentiserings- och licensbegäranden.

Om du vill lägga till fler poster i en befintlig `RevocationList`lista läser du in en befintlig lista över återkallade certifikat. Skapa en ny `RevocationListFactory` instans och se till att öka CRL-numret. Anropa `RevocationListFactioryEntries.addRevocationEntries` för att lägga till alla poster från den gamla listan i den nya listan. Anropa `RevocationListFactory.addRevocationEntry` för att lägga till nya spärrposter i RevocationList.

Exempelkod som visar hur du skapar en återkallningslista, läser in en befintlig återkallningslista och kontrollerar om en maskintoken har återkallats finns `com.adobe.flashaccess.samples.revocation.CreateRevocationList` i [!DNL samples] katalogen Reference Implementation Command Line Tools.
