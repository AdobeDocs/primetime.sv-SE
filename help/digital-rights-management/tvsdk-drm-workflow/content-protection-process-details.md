---
seo-title: Information om licensinhämtningsprocess
title: Information om licensinhämtningsprocess
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# Information om licensinhämtningsprocess {#license-acquisition-process-details}

I den här processen visas en detaljerad vy på API-nivå av arbetsflödet för skyddat DRM-innehåll i Primetime:

1. Läs in byte för det skyddade innehållets metadatafil med ett `URLLoader` objekt.

   Ange det här objektet som en variabel, till exempel `metadata_bytes`. Allt innehåll som styrs av Primetime DRM har Primetimes DRM-metadata. När innehållet paketeras kan dessa metadata sparas som en separat metadatafil ( [!DNL .metadata]) tillsammans med innehållet. Metadata kan också vara Base64-kodade och infogade i videomanifestfilen. Mer information finns i [Paketera mediefiler](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. Om det behövs tar du bort utropstecknet `!` från början av strängen.
   1. Om det behövs för HLS- eller HDS-innehåll kan du avkoda de inkluderade metadata i den Base64-kodade strängen till binära data innan du skickar den.
1. Skapa en `DRMContentData` instans.

   Placera den här koden i ett try-catch-block:

   ```
   new DRMContentData(metadata_bytes)
   ```

   där `metadata_bytes` är det `URLLoader` objekt som fås i steg 1.

   [iOS: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android: DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. Skapa avlyssnare som lyssnar efter `DRMStatusEvent` och `DRMErrorEvent` skickas från `DRMManager` objektet.

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   Kontrollera att licensen är giltig (inte null) i avlyssnaren `DRMStatusEvent` . I `DRMErrorEvent` avlyssnaren, hantera `DRMErrorEvents`. Se *Använda klassen* DRMStatusEvent och *Använda klassen* DRMErrorEvent i den här handboken.

1. Läs in licensen som krävs för att spela upp innehållet.
Försök först att läsa in en lokalt lagrad licens för att spela upp innehållet:

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android: DRMManager.obtainLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: obtainLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   När inläsningen är klar skickas `DRMManager` objektet `DRMStatusEvent.DRM_Status`.

1. Kontrollera `DRMVoucher` objektet.


   Om `DRMVoucher` objektet inte är null är licensen giltig. Gå till steg 9.

   [Android: DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS: DRMLicenseInhämtad](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. Kontrollera den autentiseringsmetod som krävs av profilen för det här innehållet.

   Använd `DRMContentData.authenticationMethod` egenskapen.
   1. Om autentiseringsmetoden är `ANONYMOUS`så gå till steg 9. 

      [Android: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS: DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. Om autentiseringsmetoden är `USERNAME_AND_PASSWORD`det måste programmet ha en funktion som gör att användaren kan ange inloggningsuppgifter.

      Skicka användarens inloggningsuppgifter till licensservern för att autentisera användaren:

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      Den `DRMManager` skickar en `DRMAuthenticationErrorEvent` if-autentisering misslyckas eller en `DRMAuthenticationCompleteEvent` if-autentisering lyckas. Skapa avlyssnare för dessa händelser.

      [Android: authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS: autentisera:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe rekommenderar att du använder en säkrare mekanism för att ange inloggningsuppgifter. Mer information finns i [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. Om autentiseringsmetoden är `UNKNOWN`det måste du använda en anpassad autentiseringsmetod.

      I det här fallet har innehållsleverantören ordnat så att autentiseringen görs utanför bandet, och inte använder Primetimes API:er. Den anpassade autentiseringsproceduren måste skapa en autentiseringstoken som kan skickas till `DRMManager.setAuthenticationToken()` metoden.

      [Android: setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS: setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >Oberoende av autentiseringsmetod kan `.setAuthenticationToken()` du också använda för att skicka anpassade data från klienten till licensservern. Detta är en överlagring av API, eftersom det här är det enda sättet att skicka dynamiska anpassade data från klienten till licensservern vid tidpunkten för licenshämtningen. Denna metod för anpassad datatransport beskrivs ingående i flera inlägg på [Primetimes DRM-forum (Adobe Access) ](https://forums.adobe.com/community/adobe_access).

1. Om autentiseringen misslyckas måste ditt program återgå till steg 6.

   Kontrollera att programmet har en mekanism som hanterar och begränsar antalet upprepade autentiseringsfel. Efter tre försök visar du till exempel ett meddelande till användaren som anger att autentiseringen har misslyckats och att innehållet inte kan spelas upp.
1. Om du vill använda den lagrade token i stället för att fråga användaren om inloggningsuppgifter anger du token med `DRMManager.setAuthenticationToken()` metoden.

   Du hämtar sedan licensen från licensservern och spelar upp innehållet som i steg 6.
   1. **Valfritt:** Om autentiseringen lyckas kan du hämta en autentiseringstoken, som är en bytearray som cachas i minnet.

      Hämta denna token med `DRMAuthenticationCompleteEvent.token` egenskapen. Du kan lagra och använda autentiseringstoken så att användaren inte behöver ange inloggningsuppgifter för det här innehållet upprepade gånger. Licensservern bestämmer giltighetsperioden för autentiseringstoken.

      [Android: OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS: DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. Om autentiseringen lyckas hämtar du licensen från licensservern:

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   När inläsningen är klar skickas `DRMManager` objektet `DRMStatusEvent.DRM_STATUS`. Lyssna efter den här händelsen och när den skickas kan du spela upp innehållet.  Spela upp videon genom att skapa ett Primetime-objekt och anropa sedan dess `play()` metod:

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android: obtainLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS: obtainLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)