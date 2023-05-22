---
description: När DRM-metadata för en video inkluderas i medieströmmen kan du utföra autentisering under uppspelningen.
title: DRM-autentisering under uppspelning
exl-id: f6e6e73a-d455-4b2c-b35c-2db173372092
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# DRM-autentisering under uppspelning {#drm-authentication-during-playback}

När DRM-metadata för en video inkluderas i medieströmmen kan du utföra autentisering under uppspelningen.

Med licensrotation krypteras en resurs med flera DRM-licenser. Varje gång nya DRM-metadata upptäcks visas `DRMHelper` metoder används för att kontrollera om DRM-metadata kräver DRM-autentisering.

>[!TIP]
>
>Innan du påbörjar uppspelningen ska du avgöra om du har att göra med en domänbunden licens och om domänautentisering krävs. Om ja, fyll i domänautentiseringen och anslut till domänen.

1. När nya DRM-metadata upptäcks i en resurs skickas en händelse i programlagret.

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. Använd `DRMMetadata` för att kontrollera om autentisering krävs.

   * Om autentisering inte krävs behöver du inte göra något, och uppspelningen fortsätter utan avbrott.
   * Om autentisering krävs, slutför DRM-autentisering.

      Eftersom den här åtgärden är asynkron och hanteras i en annan tråd påverkas inte användargränssnittet och inte heller videouppspelningen.

1. Om autentiseringen misslyckas kan användaren inte fortsätta att visa videon och uppspelningen avbryts.

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

Till exempel:

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
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
