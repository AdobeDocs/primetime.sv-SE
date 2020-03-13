---
description: Du kan vitlista dina iOS-appar med Adobes makoverktyg.
seo-description: Du kan vitlista dina iOS-appar med Adobes makoverktyg.
seo-title: Vitlista ditt iOS-program
title: Vitlista ditt iOS-program
uuid: bc558f5f-d4e6-4c1c-81eb-f8bd61c63016
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Vitlista ditt iOS-program {#whitelist-your-ios-application}

Du kan vitlista dina iOS-appar med Adobes makoverktyg.

När du slutför ett TVSDK-program kan du vanligtvis använda kommandoradsverktygen för Adobe Primetime DRM för att vitlista programmet.

>[!TIP]
>
>Du kan också använda dessa verktyg för att skapa DRM-profiler och kryptera innehåll.

Genom att vitlista appen kan du vara säker på att skyddat innehåll bara kan spelas upp i videospelaren. Vitlistning av ett iOS-program kräver dock att du slutför en speciell procedur som fungerar med Apples regler för inlämning av ansökningar.

Innan du skickar in en iOS-app måste du signera den och publicera den på Apple.

>[!NOTE]
>
>Apple rensar din utvecklares signatur och signerar om programmet med sitt eget certifikat.

På grund av den nya signeringen går det inte att använda vitlistsinformationen som du skapade innan du skickade till Apple App Store.

Adobe har skapat ett verktyg för att fingeravtryck av iOS-programmet för att skapa ett sammandragsvärde, signera det här värdet och mata in det i iOS-programmet för att kunna arbeta med den här principen. `machotools` När du har fingeravtryckt din iOS-app kan du skicka appen till Apple App Store. När en användare kör din app från App Store gör Primetime DRM en körningsberäkning av programmets fingeravtryck och bekräftar det med det sammanfattningsvärde som tidigare injicerades i programmet. Om fingeravtrycket matchar bekräftas att programmet är vitlistat och skyddat innehåll får spelas upp.

Adobe- `machotools` verktyget ingår i iOS TVSDK SDK i [!DNL [...]/tools/DRM] mapp.

Så här använder du `machotools`:

1. Skapa ett nyckelpar.

   Om du vill använda ett verktyg som OpenSSL öppnar du ett kommandofönster och anger följande:

   ```
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Ange ett lösenord för att skydda den privata nyckeln när du uppmanas till detta.

   Lösenord måste innehålla minst 12 tecken och tecknen ska innehålla en blandning av ASCII-tecken med versaler och gemener samt siffror.
1. Om du vill använda OpenSSL för att skapa ett starkt lösenord för dig öppnar du ett kommandofönster och anger följande:

   ```
   openssl rand -base64 8
   ```

1. Skapa en CSR-begäran (Certificate Signing Request).

   Om du vill använda OpenSSL för att generera en CSR-fil öppnar du ett kommandofönster och anger följande:

   ```
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Skriv under certifikatet själv och ange valfri varaktighet.

   I följande exempel visas ett utgångsdatum på 20 år:

   ```
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Konvertera det självsignerade certifikatet till en PKCS#12-fil:

   ```
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Du kan använda det självsignerade certifikatet för att signera din iOS-app.

1. Uppdatera platsen för PFX-filen och lösenordet.
1. Innan du skapar programmet i Xcode går du till **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** och lägger till följande kommando i skriptet som körs:

   ```
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Kör [!DNL machotools] för att generera hash-värdet för utgivar-ID för din app.

   ```
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Skapa en ny DRM-princip eller uppdatera din befintliga princip så att den innehåller det returnerade hash-värdet för utgivar-ID.
1. Med [!DNL AdobePolicyManager.jar]hjälp av skapar du en ny DRM-princip (uppdatera din befintliga princip) som inkluderar det returnerade värdet för utgivar-ID, ett valfritt program-ID samt lägsta och högsta versionsattributen i den inkluderade [!DNL flashaccess-tools.properties] filen.

   ```
   java -jar libs/AdobePolicyManager.jar new app_whitelist.pol
   ```

1. Paketera innehållet med den nya DRM-principen och bekräfta uppspelningen av det vitlistade innehållet i din iOS-app.