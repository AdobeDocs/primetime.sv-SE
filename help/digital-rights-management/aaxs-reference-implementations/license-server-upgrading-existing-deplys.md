---
seo-title: Uppgraderar befintliga distributioner
title: Uppgraderar befintliga distributioner
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppgraderar befintliga distributioner {#upgrading-existing-deployments}

Om du vill uppgradera en server som kör Reference Implementation License Server version 3.0 eller Watched Folder Packager ersätter du de filer som distribueras på din Application Server med de filer som ingår i Adobe Access Reference Implementation Server. [!DNL .war]

Om du tänker använda domänregistrering med Reference Implementation License Server krävs flera nya databastabeller. Kör `CreateSampleDB.sql`om du vill återskapa hela referensimplementeringsdatabasen. Om du vill bevara de befintliga databasposterna och lägga till de nya tabellerna öppnar `CreateSampleDB.sql`och kör du bara kommandona för att skapa följande tabeller:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Följande egenskaper måste läggas till i flashaccess-refimpl.properties för att domänstödet ska kunna användas:

* `HandlerConfiguration.DomainCAs.n` eller `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` och `DomainRegistrationHandler.ServerCredential.password`, eller `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Följande egenskaper måste läggas till [!DNL flashaccess-refimpl.properties] för att stöd ska kunna användas för fjärrnyckelleverans till iOS-klienter:

* `HandlerConfiguration.KeyServerCertificate` eller `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

