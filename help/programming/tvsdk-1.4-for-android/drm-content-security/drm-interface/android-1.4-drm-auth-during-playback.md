---
description: När DRM-metadata för en video inkluderas i medieströmmen ska du autentisera under uppspelningen.
seo-description: När DRM-metadata för en video inkluderas i medieströmmen ska du autentisera under uppspelningen.
seo-title: DRM-autentisering under uppspelning
title: DRM-autentisering under uppspelning
uuid: a1a63e3e-be34-49e1-96c4-ae266003b3d1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# DRM-autentisering under uppspelning {#drm-authentication-during-playback}

När DRM-metadata för en video inkluderas i medieströmmen ska du autentisera under uppspelningen.

Ta en titt på licensrotationsfunktionen, där en resurs krypteras med flera DRM-licenser. Varje gång nya DRM-metadata upptäcks använder du `DRMHelper` metoder för att kontrollera om DRM-metadata kräver DRM-autentisering.

>[!NOTE]
>
>Den här självstudiekursen hanterar inte domänbundna licenser. Innan du påbörjar uppspelningen bör du helst kontrollera om du har att göra med en domänbunden licens. Om ja, utför domänautentisering (om det behövs) och anslut till domänen.

1. När nya DRM-metadata upptäcks i en resurs skickas en händelse i programlagret.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. Använd för `DRMMetadata` att kontrollera om autentisering behövs. Om inte, gör ingenting; uppspelningen fortsätter utan avbrott.
1. Annars måste du utföra DRM-autentisering. Eftersom den här åtgärden är asynkron och hanteras i en annan tråd påverkas inte användargränssnittet och inte heller videouppspelningen.
1. Om autentiseringen misslyckas kan användaren inte fortsätta att visa videon och uppspelningen avbryts. I annat fall fortsätter uppspelningen oavbrutet.

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
        }); 
    } 
};
```
