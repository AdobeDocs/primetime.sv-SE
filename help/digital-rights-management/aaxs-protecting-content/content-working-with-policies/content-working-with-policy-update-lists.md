---
title: Arbeta med principuppdateringslistor
description: Arbeta med principuppdateringslistor
copied-description: true
exl-id: 71715eec-e6a3-4640-b17f-ec0c38caf73e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Arbeta med principuppdateringslistor{#working-with-policy-update-lists}

För licensservrar som inte har tillgång till en databas för att lagra information om profiler kan du använda en principuppdateringslista för att meddela licensservern om uppdaterade profiler. Listor för principuppdatering kan innehålla uppdaterade versioner av profiler eller en lista med princip-ID:n som har återkallats. Om en principuppdateringslista anges i `HandlerConfiguration`kommer SDK att tillämpa den här listan när en licens utfärdas.

Profiler kan också återkallas om innehållsägare eller distributörer vill upphöra med att utfärda licenser enligt en viss policy. En principuppdateringslista kan användas för att framtvinga återkallad princip i SDK. Listor för principuppdatering kan också användas för att tillhandahålla en lista med uppdaterade profiler till SDK. Observera att återkallande av en profil inte medför återkallande av licenser som redan har utfärdats. Det förhindrar bara att ytterligare licenser utfärdas enligt den policyn.

När du arbetar med listor för principuppdatering används en `PolicyUpdateListFactory` -objekt. Så här skapar du en principuppdateringslista, läser in en befintlig principuppdateringslista och kontrollerar om en princip har uppdaterats eller återkallats med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i Konfigurera utvecklingsmiljön i ditt projekt.
1. Skapa en `ServerCredentialFactory` -instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `PolicyUpdateListFactory` -instans med `ServerCredential` du skapade.
1. Ange det princip-ID som ska återkallas.
1. Skapa en `PolicyRevocationEntry` objekt som använder princip-ID `String` du har skapat och lagt till den i listan över principuppdateringar genom att skicka den till `PolicyUpdateListFactory.addRevocationEntry()`. Generera den nya principuppdateringslistan genom att ringa `PolicyUpdateListFactory.generatePolicyUpdateList()`. På samma sätt kan uppdaterade profiler läggas till i listan med `PolicyUpdateEntry`.
1. Om det redan finns en principuppdateringslista kan du serialisera den för inläsning genom att anropa `PolicyUpdateList.getBytes()`. Om du vill läsa in listan ringer du `PolicyUpdateListFactory.loadPolicyUpdateList()` och skicka i den serialiserade listan.
1. Kontrollera att signaturen är giltig och att listan signerades av rätt licensservercertifikat genom att anropa `PolicyUpdateList.verifySignature()`.
1. Om du vill kontrollera om en post har återkallats skickar du princip-ID:t `String` till `PolicyUpdateList.isRevoked()`. Listan kan även skickas till `HandlerConfiguration` och kommer att verkställas när licenserna utfärdas.

Lägga till fler poster i en befintlig `PolicyUpdateList`, läser in en befintlig principuppdateringslista. Skapa ett nytt `PolicyUpdateListFactory` -instans. Utlysning P `olicyUpdateListFactory.addEntries` om du vill lägga till alla poster från den gamla listan i den nya listan. Utlysning `PolicyUpdateListFactory.addRevocationEntry` eller `addUpdatedEntry` om du vill lägga till nya återkallnings- eller uppdateringsposter i PolicyUpdateList.

Exempelkod som visar hur du skapar en principuppdateringslista, läser in en befintlig principuppdateringslista och kontrollerar om en princip har återkallats finns i `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.
