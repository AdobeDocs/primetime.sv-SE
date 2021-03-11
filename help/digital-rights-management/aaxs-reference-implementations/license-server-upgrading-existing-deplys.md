---
title: Uppgraderar befintliga distributioner
description: Uppgraderar befintliga distributioner
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Uppgraderar befintliga distributioner {#upgrading-existing-deployments}

Om du vill uppgradera en server som kör referensimplementeringslicensservern version 3.0 eller Packager för bevakad mapp ersätter du [!DNL .war]-filerna som distribueras på programservern med filerna som ingår i referensimplementeringsservern för Adobe Access.

Om du tänker använda domänregistrering med Reference Implementation License Server krävs flera nya databastabeller. Kör `CreateSampleDB.sql` om du vill återskapa hela referensimplementeringsdatabasen. Om du vill bevara de befintliga databasposterna och lägga till de nya tabellerna öppnar du `CreateSampleDB.sql`och kör bara kommandona för att skapa följande tabeller:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

Följande egenskaper måste läggas till i flashaccess-refimpl.properties för att domänstödet ska kunna användas:

* `HandlerConfiguration.DomainCAs.n` eller  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` och  `DomainRegistrationHandler.ServerCredential.password`, eller  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

Följande egenskaper måste läggas till i [!DNL flashaccess-refimpl.properties] för att stöd ska kunna användas för fjärrnyckelleverans till iOS-klienter:

* `HandlerConfiguration.KeyServerCertificate` eller  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

