---
description: Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.
keywords: regler för kreativt urval;AdobeTVSDKConfig;ad creative priority;transformeringsregler
title: Uppdatera och skapa regler för urval
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Ökning {#updating-ad-creative-selection-rules-overview}

Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.

När videospelaren skickar en begäran till en annonsserver innehåller VAST/VMAP-svaret vanligtvis flera annonsskapare ( `MediaFile` -element) som vart och ett tillhandahåller en URL till en annan behållar-kodek-version. I vissa fall kan annonskreatörer i VAST/VMAP-svaret ge olika bithastighet för annonsen. Om du vill ange din egen prioritet och omformningsregler för dessa annonskreatörer kan du göra det i [!DNL AdobeTVSDKConfig.json] konfigurationsfil.

>[!IMPORTANT]
>
>* Ändra inte namnet på TVSDK-konfigurationsfilen. Namnet måste finnas kvar [!DNL AdobeTVSDKConfig.json].
>* Den här filen måste placeras i [!DNL assets/] projektmapp.
>

Du kan ange två typer av regler i [!DNL AdobeTVSDKConfig.json]: *Prioritet* regler och *Normalisera* regler.

## Inaktiverar förrullning {#disabling-preroll}

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
