---
description: Om du vill uppgradera en server som stöder Reference Implementation License Server version 3.0 eller Watched Folder Packager måste du ersätta de .war-filer som har distribuerats på en Application Server med de filer som har inkluderats i Adobe Primetime DRM Reference Implementation Server.
title: Uppgradera befintliga distributioner
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

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

1. Lägg till följande egenskaper i [!DNL flashaccess-refimpl.properties] för att använda domänstödet:

   * `HandlerConfiguration.DomainCAs.n` eller `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` och `DomainRegistrationHandler.ServerCredential.password` eller `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Lägg till följande egenskaper i [!DNL flashaccess-refimpl.properties] för att ge stöd åt fjärråtkomstleverans till iOS-klienter:

   * `HandlerConfiguration.KeyServerCertificate` eller `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
