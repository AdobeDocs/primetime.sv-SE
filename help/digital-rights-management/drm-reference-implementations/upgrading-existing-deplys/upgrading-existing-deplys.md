---
description: Om du vill uppgradera en server som stöder Reference Implementation License Server version 3.0 eller Watched Folder Packager måste du ersätta de .war-filer som har distribuerats på en Application Server med de filer som har inkluderats i Adobe Primetime DRM Reference Implementation Server.
seo-description: Om du vill uppgradera en server som stöder Reference Implementation License Server version 3.0 eller Watched Folder Packager måste du ersätta de .war-filer som har distribuerats på en Application Server med de filer som har inkluderats i Adobe Primetime DRM Reference Implementation Server.
seo-title: Uppgradera befintliga distributioner
title: Uppgradera befintliga distributioner
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Översikt {#upgrade-existing-deployments-overview}

Om du vill uppgradera en server som stöder Reference Implementation License Server version 3.0 eller Watched Folder Packager måste du ersätta de .war-filer som har distribuerats på en Application Server med de filer som har inkluderats i Adobe Primetime DRM Reference Implementation Server.

Om du vill använda domänregistrering med Reference Implementation License Server krävs flera nya databastabeller. Du måste återskapa hela referensimplementeringsdatabasen och köra `CreateSampleDB.sql`.

Så här bevarar du databasposter och lägger till nya tabeller:

1. Öppna `CreateSampleDB.sql` och köra kommandon som skapar följande tabeller:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Lägg till följande egenskaper för [!DNL flashaccess-refimpl.properties] att använda domänstödet:

   * `HandlerConfiguration.DomainCAs.n` eller `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` och `DomainRegistrationHandler.ServerCredential.password` eller `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Lägg till följande egenskaper för [!DNL flashaccess-refimpl.properties] att ge stöd för fjärrnyckelleverans till iOS-klienter:

   * `HandlerConfiguration.KeyServerCertificate` eller `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`