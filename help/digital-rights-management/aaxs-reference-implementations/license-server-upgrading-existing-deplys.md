---
title: Uppgraderar befintliga distributioner
description: Uppgraderar befintliga distributioner
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Uppgraderar befintliga distributioner {#upgrading-existing-deployments}

Om du vill uppgradera en server som kör referensimplementeringslicensservern eller Packager för version 3.0 ska du ersätta [!DNL .war] filer som distribueras på din programserver med de filer som ingår i Adobe Access Reference Implementation Server.

Om du tänker använda domänregistrering med Reference Implementation License Server krävs flera nya databastabeller. Om du vill återskapa hela referensimplementeringsdatabasen kör du `CreateSampleDB.sql`. Om du vill bevara de befintliga databasposterna och lägga till de nya tabellerna öppnar du `CreateSampleDB.sql`och kör bara kommandona för att skapa följande tabeller:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Följande egenskaper måste läggas till i flashaccess-refimpl.properties för att domänstödet ska kunna användas:

* `HandlerConfiguration.DomainCAs.n` eller `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` och `DomainRegistrationHandler.ServerCredential.password`, eller `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Följande egenskaper måste läggas till i [!DNL flashaccess-refimpl.properties] för att ge stöd åt fjärråtkomstleverans till iOS-klienter:

* `HandlerConfiguration.KeyServerCertificate` eller `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
