---
title: Konfigurera och distribuera servern för skyddad strömning
description: Konfigurera och distribuera servern för skyddad strömning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Konfigurera och distribuera servern för skyddad strömning {#set-up-and-deploy-the-server-for-protected-streaming}

1. Konfigurera konfigurationsmappen på Primetime DRM DVD:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Kopiera exemplet `configs` mapp till `<Tomcat_installation_dir>` och ändra namn på den kopierade mappen till `licenseserver`.

   Sökvägen till konfigurationsmappen bör nu vara `<Tomcat_install_dir>\licenseserver\`.
1. Kör `Scrambler.bat` för att få krypterade lösenord för transport- och licensserverns PFX-filer i Primetimes DRM `<DVD>` `\Adobe Access Server for Protected Streaming\` katalog:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Kopiera PFX-filerna till `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` katalog.
1. Redigera motsvarande klientkonfiguration i `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, med följande inställningar:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Kör `Validator.bat` verktyg för att verifiera konfigurationen är giltigt:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Kopiera `flashaccessserver.war` från CD:n till `<TomcatInstallDir>\webapps\` katalog.
1. Om Tomcat körs stoppar du den Tomcat-instans som körs genom att trycka på `<CTRL-C>` i kommandofönstret (om det startades från kommandofönstret). Du kan också stoppa servern från Windows Services-programmet om Tomcat installerades som en Windows-tjänst.
1. Starta Tomcat genom att ange följande kommando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Verifiera konfigurationen genom att ange följande URL i en webbläsare:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
