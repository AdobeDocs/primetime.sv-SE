---
seo-title: Arbeta med principuppdateringslistor
title: Arbeta med principuppdateringslistor
uuid: 583abb31-5c80-43f2-bc3d-a2300f61c4ea
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Arbeta med principuppdateringslistor{#working-with-policy-update-lists}

För licensservrar som inte har tillgång till en databas för att lagra information om profiler kan du använda en principuppdateringslista för att meddela licensservern om uppdaterade profiler. Listor för principuppdatering kan innehålla uppdaterade versioner av profiler eller en lista med princip-ID:n som har återkallats. Om en principuppdateringslista anges i `HandlerConfiguration`kommer SDK att tillämpa den här listan när en licens utfärdas.

Profiler kan också återkallas om innehållsägare eller distributörer vill upphöra med att utfärda licenser enligt en viss policy. En principuppdateringslista kan användas för att framtvinga återkallad princip i SDK. Listor för principuppdatering kan också användas för att tillhandahålla en lista med uppdaterade profiler till SDK. Observera att återkallande av en profil inte medför återkallande av licenser som redan har utfärdats. Det förhindrar bara att ytterligare licenser utfärdas enligt den policyn.

När du arbetar med principuppdateringslistor används ett `PolicyUpdateListFactory` objekt. Så här skapar du en principuppdateringslista, läser in en befintlig principuppdateringslista och kontrollerar om en princip har uppdaterats eller återkallats med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i Konfigurera utvecklingsmiljön i ditt projekt.
1. Skapa en `ServerCredentialFactory` instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `PolicyUpdateListFactory` instans med hjälp av den `ServerCredential` du skapade.
1. Ange det princip-ID som ska återkallas.
1. Skapa ett `PolicyRevocationEntry` objekt med det princip-ID som `String` du nyss skapade och lägg till det i principuppdateringslistan genom att skicka det till `PolicyUpdateListFactory.addRevocationEntry()`. Generera den nya principuppdateringslistan genom att ringa `PolicyUpdateListFactory.generatePolicyUpdateList()`. På samma sätt kan uppdaterade profiler läggas till i listan med `PolicyUpdateEntry`.
1. Om det redan finns en principuppdateringslista kan du serialisera den för inläsning genom att anropa `PolicyUpdateList.getBytes()`. Om du vill läsa in listan anropar du `PolicyUpdateListFactory.loadPolicyUpdateList()` och skickar den serialiserade listan.
1. Kontrollera att signaturen är giltig och att listan signerades av rätt licensservercertifikat genom att ringa `PolicyUpdateList.verifySignature()`.
1. Om du vill kontrollera om en post har återkallats skickar du princip-ID:t `String` till `PolicyUpdateList.isRevoked()`. Listan kan också skickas till `HandlerConfiguration` och tillämpas när licenser utfärdas.

Om du vill lägga till fler poster i en befintlig `PolicyUpdateList`principuppdateringslista läser du in en befintlig principuppdateringslista. Skapa en ny `PolicyUpdateListFactory` instans. Ring P om du `olicyUpdateListFactory.addEntries` vill lägga till alla poster från den gamla listan i den nya listan. Anropa `PolicyUpdateListFactory.addRevocationEntry` eller `addUpdatedEntry` lägga till nya återkallnings- eller uppdateringsposter i PolicyUpdateList.

Exempelkod som visar hur du skapar en principuppdateringslista, läser in en befintlig principuppdateringslista och kontrollerar om en princip har återkallats finns `com.adobe.flashaccess.samples.policyupdatelist``.CreatePolicyUpdateList` i katalogen&quot;samples&quot; (Exempel) i kommandoradsverktygen för referensimplementering.
