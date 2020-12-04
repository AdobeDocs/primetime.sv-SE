---
description: När DRM-metadata för en video är åtskilda från medieströmmen ska du autentisera innan uppspelningen börjar.
seo-description: När DRM-metadata för en video är åtskilda från medieströmmen ska du autentisera innan uppspelningen börjar.
seo-title: DRM-autentisering före uppspelning
title: DRM-autentisering före uppspelning
uuid: 326ef93d-53b0-4e3a-b16d-f3b886837cc0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---


# DRM-autentisering före uppspelning {#drm-authentication-before-playback}

När DRM-metadata för en video är åtskilda från medieströmmen ska du autentisera innan uppspelningen börjar.

En videoresurs kan ha en associerad DRM-metadatafil. Exempel:

* &quot;url&quot;: &quot;ht<span></span>tps://www.domain.com/asset.m3u8&quot;
* &quot;drmMetadata&quot;: &quot;ht<span></span>tps://www.domain.com/asset.metadata&quot;

I så fall använder du `DRMHelper`-metoder för att hämta innehållet i DRM-metadatafilen, tolka den och kontrollera om DRM-autentisering krävs.

1. Använd `loadDRMMetadata` för att läsa in URL-metadatainnehållet och tolka de hämtade byten till en `DRMMetadata`.

   I likhet med andra nätverksåtgärder är den här metoden asynkron och skapar en egen tråd.

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   Exempel:

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. Eftersom åtgärden är asynkron är det en bra idé att informera användaren om det. Annars kommer han att undra varför hans uppspelning inte börjar. Du kan till exempel visa ett rotationshjul medan DRM-metadata hämtas och tolkas.
1. Implementera återanropen i `DRMLoadMetadataListener`. `loadDRMMetadata` anropar dessa händelsehanterare (skickar dessa händelser).

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

   * `onLoadMetadataUrlStart` identifierar när inläsningen av metadata-URL har påbörjats.
   * `onLoadMetadataUrlComplete` identifierar när metadata-URL:en har lästs in.
   * `onLoadMetadataUrlError` anger att det inte gick att läsa in metadata.

1. När inläsningen är klar kontrollerar du `DRMMetadata`-objektet för att se om DRM-autentisering behövs.

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. Om autentisering inte krävs börjar uppspelningen.
1. Om autentisering krävs utför du autentiseringen genom att hämta licensen.

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

   Det här exemplet kodar för enkelhetens skull användarens namn och lösenord.

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   ```

1. Detta innebär även nätverkskommunikation, och därför är detta också en asynkron åtgärd. Använd en händelseavlyssnare för att kontrollera autentiseringsstatusen.

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   ```

1. Starta uppspelningen om autentiseringen lyckas.
1. Om autentiseringen inte lyckas kontaktar du användaren och startar inte uppspelningen.

Programmet måste hantera eventuella autentiseringsfel. Det gick inte att autentisera innan TVSDK spelas upp. Detta leder till ett feltillstånd. Det innebär att dess status ändras till FEL, att ett fel genereras som innehåller felkoden från DRM-biblioteket och att uppspelningen stoppas. Programmet måste lösa problemet, återställa spelaren och läsa in resursen igen.

