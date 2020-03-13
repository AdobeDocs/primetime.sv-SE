---
description: När DRM-metadata för en video är separata från medieströmmen bör du autentisera innan du påbörjar uppspelningen.
seo-description: När DRM-metadata för en video är separata från medieströmmen bör du autentisera innan du påbörjar uppspelningen.
seo-title: DRM-autentisering före uppspelning
title: DRM-autentisering före uppspelning
uuid: be319b04-a506-4278-8275-db32cd3f18aa
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# DRM-autentisering före uppspelning {#drm-authentication-before-playback}

När DRM-metadata för en video är separata från medieströmmen bör du autentisera innan du påbörjar uppspelningen.

En videoresurs kan ha en associerad DRM-metadatafil, till exempel:

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

I det här exemplet kan du använda `DRMHelper` metoder för att hämta innehållet i DRM-metadatafilen, tolka den och kontrollera om DRM-autentisering behövs.

1. Använd `loadDRMMetadata` för att läsa in URL-metadatainnehållet och tolka de hämtade byten till en `DRMMetadata`.

   >[!TIP]
   >
   >Den här metoden är asynkron och skapar en egen tråd.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Exempel:

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. Meddela användaren om att den här åtgärden är asynkron. Det är en bra idé att informera användaren om det.

   Om användarna inte vet om åtgärden är asynkron kan de undra varför uppspelningen ännu inte har startats. Du kan till exempel visa ett rotationshjul medan DRM-metadata hämtas och tolkas.

1. Implementera återanropen i `DRMLoadMetadataListener`.

       &quot;loadDRMMetadata&quot; anropar dessa händelsehanterare.
       
 &quot;java     
 public interface DRMLoadMetadataListener {     
     
     public void onLoadMetadataUrlStart();
       
     /**
     * @param authNeeded
     * huruvida DRM-autentisering krävs.
       * @param drmMetadata
     * de tolkade DRMMetadata som erhållits.    */
 public     void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata);
   public     void onLoadMetadataUrlError();
       }
     
     &quot;
     
     Här finns mer information om hanterarna:
   
   * `onLoadMetadataUrlStart` identifierar när inläsningen av metadata-URL har påbörjats.
   * `onLoadMetadataUrlComplete` identifierar när metadata-URL:en har lästs in.
   * `onLoadMetadataUrlError` anger att det inte gick att läsa in metadata.

1. När inläsningen är klar kontrollerar du objektet för att se om det krävs någon DRM-autentisering `DRMMetadata` .

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   Exempel:

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. Gör något av följande:

   * Om ingen autentisering krävs börjar uppspelningen.
   * Om autentisering krävs slutför du autentiseringen genom att hämta licensen.

      ```java
      /** 
      * Helper method to perform DRM authentication. 
      * 
      * @param drmManager 
      * the DRMManager, used to perform the authentication. 
      * @param drmMetadata 
      * the DRMMetadata, containing the DRM specific information. 
      * @param authenticationListener 
      * the listener, on which the user can be notified about the 
      * authentication process status. 
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      I det här exemplet kodas användarens namn och lösenord uttryckligen:

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. Använd en händelseavlyssnare för att kontrollera autentiseringsstatusen.

   Den här processen innebär nätverkskommunikation, så det här är också en asynkron åtgärd.

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. Om autentiseringen lyckas startar du uppspelningen.
1. Om autentiseringen inte lyckas kontaktar du användaren och startar inte uppspelningen.

   Programmet måste hantera eventuella autentiseringsfel. Om det inte går att autentisera innan TVSDK spelas upp placeras det i ett feltillstånd och uppspelningen stoppas. Programmet måste lösa problemet, återställa spelaren och läsa in resursen igen.