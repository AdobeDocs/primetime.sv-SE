---
description: Du kan tillåtelselista era iOS-appar med Adobe Machotools.
title: Tillåtelselista ditt iOS-program
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Tillåtelselista ditt iOS-program {#allowlist-your-ios-application}

Du kan tillåtelselista era iOS-appar med Adobe Machotools.

När du slutför ett TVSDK-program kan du vanligtvis använda kommandoradsverktygen i Adobe Primetime DRM för att tillåtelselista din app.

>[!TIP]
>
>Du kan också använda dessa verktyg för att skapa DRM-profiler och kryptera innehåll.

Tillåt att appen listas så att skyddat innehåll endast kan spelas upp i videospelaren. Tillåt att ett iOS-program listas kräver dock att du slutför en särskild procedur som fungerar med Apple regler för att skicka in program.

Innan du skickar in en iOS-app måste du signera den och publicera den på Apple.

>[!NOTE]
>
>Apple rensar din utvecklares signatur och signerar om programmet med sitt eget certifikat.

På grund av den nya signeringen går det inte att använda den tillståndslistinformation som du genererade innan du skickade till Apple App Store.

Adobe har skapat en `machotools` verktyg som fingeravtrycksändrar ditt iOS-program för att skapa ett sammanfattningsvärde, signera värdet och mata in värdet i ditt iOS-program. När du har fingeravtryckt din iOS-app kan du skicka den till Apple App Store. När en användare kör din app från App Store gör Primetime DRM en körningsberäkning av programmets fingeravtryck och bekräftar det med det sammanfattningsvärde som tidigare injicerades i programmet. Om fingeravtrycket matchar bekräftas att programmet är tillåtet i listan och skyddat innehåll får spelas upp.

Adobe `machotools` finns i iOS TVSDK SDK i [!DNL [...]/tools/DRM] mapp.

Används `machotools`:

1. Skapa ett nyckelpar.

   Om du vill använda ett verktyg som OpenSSL öppnar du ett kommandofönster och anger följande:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Ange ett lösenord för att skydda den privata nyckeln när du uppmanas till detta.

   Lösenord måste innehålla minst 12 tecken och tecknen ska innehålla en blandning av ASCII-tecken med versaler och gemener samt siffror.
1. Om du vill använda OpenSSL för att skapa ett starkt lösenord för dig öppnar du ett kommandofönster och anger följande:

   ```shell
   openssl rand -base64 8
   ```

1. Skapa en CSR-begäran (Certificate Signing Request).

   Om du vill använda OpenSSL för att generera en CSR-fil öppnar du ett kommandofönster och anger följande:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Skriv under certifikatet själv och ange valfri varaktighet.

   I följande exempel visas ett utgångsdatum på 20 år:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Konvertera det självsignerade certifikatet till en PKCS#12-fil:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Du kan använda det självsignerade certifikatet för att signera din iOS-app.

1. Uppdatera platsen för PFX-filen och lösenordet.
1. Innan du skapar programmet i Xcode ska du gå till  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** och lägg till följande kommando i körningsskriptet:

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Kör [!DNL machotools] för att generera hash-värdet för ditt utgivar-ID för programmet.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Skapa en ny DRM-princip eller uppdatera din befintliga princip så att den innehåller det returnerade hash-värdet för utgivar-ID.
1. Använda [!DNL AdobePolicyManager.jar]skapar du en ny DRM-princip (uppdatera din befintliga princip) som inkluderar det returnerade värdet för utgivar-ID, ett valfritt program-ID och lägsta och högsta versionsattributen i det inkluderade [!DNL flashaccess-tools.properties] -fil.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Paketera innehållet med den nya DRM-principen och bekräfta uppspelningen av det tillåtna innehållet i din iOS-app.
