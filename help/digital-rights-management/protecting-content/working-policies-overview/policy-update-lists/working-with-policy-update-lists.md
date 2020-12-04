---
seo-title: Arbeta med DRM-principuppdateringslistor
title: Arbeta med DRM-principuppdateringslistor
uuid: 41f89671-81c6-4d3d-ac31-9c2a1980517a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# Uppdateringslistor för DRM-princip {#drm-policy-update-lists}

Om du uppdaterar användningsreglerna i en DRM-profil efter att ha paketerat något innehåll måste licensservern ha den senaste versionen innan den kan utfärda licenser som använder en uppdaterad DRM-princip. Ett sätt att uppnå detta är genom en uppdateringslista för DRM-principen.

En uppdateringslista för en DRM-princip representeras av en fil som innehåller en lista över uppdaterade eller återkallade DRM-principer. När du uppdaterar en DRM-princip måste du generera en ny DRM-principuppdateringslista och regelbundet skicka listan till alla licensservrar.

## Arbeta med DRM-principuppdateringslistor {#working-with-drm-policy-update-lists}

För licensservrar som inte har tillgång till en databas för lagring av information om DRM-principer kan du använda en uppdateringslista för DRM-principen för att meddela licensservern om uppdaterade DRM-principer. DRM-principuppdateringslistor kan innehålla uppdaterade versioner av DRM-principer eller en lista över DRM-princip-ID:n som har återkallats. Om en principuppdateringslista ingår i `HandlerConfiguration` verkställer SDK den här listan när den utfärdar en licens.

Du kan också återkalla DRM-profiler om innehållsägare eller distributörer vill sluta utfärda licenser enligt en viss DRM-princip. En uppdateringslista för DRM-principer kan användas för att framtvinga återkallning av DRM-principer i SDK. Du kan också använda listor för DRM-principuppdatering för att visa en lista över uppdaterade DRM-principer för SDK.

>[!NOTE]
>
>När du återkallar en DRM-princip återkallas inte automatiskt de licenser som redan har utfärdats. Det förhindrar bara att ytterligare licenser utfärdas enligt DRM-principen.

## Uppdatera principuppdateringslistor{#update-policy-update-lists}

När du arbetar med uppdateringslistor för DRM-principer används ett `PolicyUpdateListFactory`-objekt. Om du vill skapa en uppdateringslista för en DRM-princip måste du läsa in en befintlig uppdateringslista för DRM-principen och sedan kontrollera om en DRM-princip har uppdaterats eller återkallats med Java API.

Så här arbetar du med DRM-principuppdateringslistor:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som ingår när du konfigurerar utvecklingsmiljön i ett projekt.
1. Skapa en `ServerCredentialFactory`-instans för att läsa in de autentiseringsuppgifter som krävs för signering.
1. Skapa en `PolicyUpdateListFactory`-instans med `ServerCredential` som du skapade.
1. Ange det DRM-princip-ID som du vill återkalla.
1. Skapa ett `PolicyRevocationEntry`-objekt med hjälp av DRM-princip-ID:t `String` som du nyss skapade och lägg sedan till det i DRM-principuppdateringslistan genom att skicka det till `PolicyUpdateListFactory.addRevocationEntry()`.
1. Generera den nya uppdateringslistan för DRM-principen genom att anropa `PolicyUpdateListFactory.generatePolicyUpdateList()`.

   På samma sätt kan du uppdatera DRM-profiler till listan med `PolicyUpdateEntry`.
1. Om det redan finns en uppdateringslista för DRM-principen kan du serialisera den för inläsning genom att anropa `PolicyUpdateList.getBytes()`.

   Om du vill läsa in listan ringer du `PolicyUpdateListFactory.loadPolicyUpdateList()` och skickar den i den serialiserade listan.
1. Kontrollera att signaturen är giltig och att listan har signerats av rätt licensservercertifikat genom att ringa `PolicyUpdateList.verifySignature()`.
1. Skicka DRM-principens ID `String` till `PolicyUpdateList.isRevoked()` för att verifiera att en post har återkallats.

   Du kan också skicka listan till `HandlerConfiguration` där den sedan används när licenser utfärdas.
Om du vill lägga till fler poster i en befintlig `PolicyUpdateList` måste du läsa in en befintlig DRM-principuppdateringslista. Därför måste du skapa en ny DRM `PolicyUpdateListFactory`-instans. Ring `PolicyUpdateListFactory.addEntries` om du vill lägga till alla poster från den gamla listan i den nya listan. Anropa `PolicyUpdateListFactory.addRevocationEntry` eller `addUpdatedEntry` för att lägga till nya återkallnings- eller uppdateringsposter i DRM PolicyUpdateList.

Exempelkod som visar hur du skapar en uppdateringslista för en DRM-princip finns i `com.adobe.flashaccess.samples.policyupdatelist` `.CreatePolicyUpdateList` i *Command Line Tools för referensimplementering* [!DNL samples]-katalogen.
