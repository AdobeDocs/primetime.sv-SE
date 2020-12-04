---
seo-title: Uppgraderar befintliga distributioner
title: Uppgraderar befintliga distributioner
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
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

