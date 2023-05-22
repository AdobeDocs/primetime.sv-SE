---
title: Arbeta med DRM-principuppdateringslistor
description: Arbeta med DRM-principuppdateringslistor
copied-description: true
exl-id: 140f1fff-2078-427b-ade2-8ec18a14216f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Uppdateringslistor för DRM-princip {#drm-policy-update-lists}

Om du uppdaterar användningsreglerna i en DRM-profil efter att ha paketerat något innehåll måste licensservern ha den senaste versionen innan den kan utfärda licenser som använder en uppdaterad DRM-princip. Ett sätt att uppnå detta är genom en uppdateringslista för DRM-principen.

En uppdateringslista för en DRM-princip representeras av en fil som innehåller en lista över uppdaterade eller återkallade DRM-principer. När du uppdaterar en DRM-princip måste du generera en ny DRM-principuppdateringslista och regelbundet skicka listan till alla licensservrar.

## Arbeta med DRM-principuppdateringslistor {#working-with-drm-policy-update-lists}

För licensservrar som inte har tillgång till en databas för lagring av information om DRM-principer kan du använda en uppdateringslista för DRM-principen för att meddela licensservern om uppdaterade DRM-principer. DRM-principuppdateringslistor kan innehålla uppdaterade versioner av DRM-principer eller en lista över DRM-princip-ID:n som har återkallats. Om en principuppdateringslista ingår i `HandlerConfiguration`, kommer SDK att tillämpa den här listan när den utfärdar en licens.

Du kan också återkalla DRM-profiler om innehållsägare eller distributörer vill sluta utfärda licenser enligt en viss DRM-princip. En uppdateringslista för DRM-principer kan användas för att framtvinga återkallning av DRM-principer i SDK. Du kan också använda listor för DRM-principuppdatering för att visa en lista över uppdaterade DRM-principer för SDK.

>[!NOTE]
>
>När du återkallar en DRM-princip återkallas inte automatiskt de licenser som redan har utfärdats. Det förhindrar bara att ytterligare licenser utfärdas enligt DRM-principen.

## Uppdatera principuppdateringslistor{#update-policy-update-lists}

När du arbetar med uppdateringslistor för DRM-principer används en `PolicyUpdateListFactory` -objekt. Om du vill skapa en uppdateringslista för en DRM-princip måste du läsa in en befintlig uppdateringslista för DRM-principen och sedan kontrollera om en DRM-princip har uppdaterats eller återkallats med Java API.

Så här arbetar du med DRM-principuppdateringslistor:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som ingår när du konfigurerar utvecklingsmiljön i ett projekt.
1. Skapa en `ServerCredentialFactory` -instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `PolicyUpdateListFactory` -instans med `ServerCredential` som du skapade.
1. Ange det DRM-princip-ID som du vill återkalla.
1. Skapa en `PolicyRevocationEntry` objekt med hjälp av DRM-princip-ID `String` som du just har skapat och sedan lagt till den i DRM-principuppdateringslistan genom att skicka den till `PolicyUpdateListFactory.addRevocationEntry()`.
1. Generera den nya uppdateringslistan för DRM-principen genom att anropa `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   På samma sätt kan du uppdatera DRM-profiler till listan med `PolicyUpdateEntry`.
1. Om det redan finns en uppdateringslista för DRM-principen kan du serialisera den för inläsning genom att anropa `PolicyUpdateList.getBytes()`.

   Om du vill läsa in listan ringer du `PolicyUpdateListFactory.loadPolicyUpdateList()` och skicka det i den serialiserade listan.
1. Verifiera att signaturen är giltig och att listan har signerats av rätt licensservercertifikat genom att anropa `PolicyUpdateList.verifySignature()`.
1. Skicka DRM-princip-ID `String` till `PolicyUpdateList.isRevoked()` för att verifiera att en post har återkallats.

   Du kan också skicka listan till `HandlerConfiguration` där det sedan tillämpas när licenser utfärdas.
Om du vill lägga till fler poster i en befintlig `PolicyUpdateList`måste du läsa in en befintlig DRM-principuppdateringslista. Därför måste du skapa ett nytt DRM `PolicyUpdateListFactory` -instans. Utlysning `PolicyUpdateListFactory.addEntries` om du vill lägga till alla poster från den gamla listan i den nya listan. Utlysning `PolicyUpdateListFactory.addRevocationEntry` eller `addUpdatedEntry` om du vill lägga till nya återkallnings- eller uppdateringsposter i DRM PolicyUpdateList.

Exempelkod som visar hur du skapar en uppdateringslista för en DRM-princip finns i `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` i *Kommandoradsverktyg för implementering* [!DNL samples] katalog.
