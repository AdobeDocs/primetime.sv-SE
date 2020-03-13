---
description: Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.
seo-title: Uppdatera och skapa regler för urval
title: Uppdatera och skapa regler för urval
uuid: c33fe1f0-78cb-4dc2-89d2-e9fb1bf0e73f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Översikt {#update-ad-creative-selection-rules-overview}

Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.

När videospelaren skickar en begäran till en annonsserver innehåller VAST/VMAP-svaret vanligtvis flera annonsskapare ( `MediaFile` element), som var och en tillhandahåller en URL till en annan behållar-kodekversion. I vissa fall kan annonskreatörer i VAST/VMAP-svaret ge olika bithastighet för annonsen. Om du vill ange din egen prioritet och omformningsregler för dessa annonskreatörer kan du göra det i [!DNL AdobeTVSDKConfig.json] konfigurationsfilen.

>[!IMPORTANT]
>
>* Ändra inte namnet på TVSDK-konfigurationsfilen. Namnet måste finnas kvar [!DNL AdobeTVSDKConfig.json].
>* Du kan montera den här filen var som helst som är tillgänglig för ditt paket.
>



Du kan ange två typer av regler i [!DNL AdobeTVSDKConfig.json]: *Prioritetsregler* och *Normalisera* regler.

**[!UICONTROL Disabling Pre-Roll]**

Om du vill inaktivera förregistrering måste du ändra standardgeneratorerna för affärsmöjlighet så att de inte gör förrollsanropet. Som standard använder TVSDK följande generatorer för affärstillfällen:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

Om du vill inaktivera förregistrering för liveströmmar bör detta ändras så att endast SpliceOutOpportunityGenerator ingår:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```

