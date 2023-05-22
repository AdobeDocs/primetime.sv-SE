---
description: Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.
keywords: regler för kreativt urval;AdobeTVSDKConfig;ad creative priority;transformeringsregler
title: Uppdatera och skapa regler för urval
exl-id: b4249936-d658-49fb-85af-ebd8e1211d55
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Översikt {#update-ad-creative-selection-rules-overview}

Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.

När videospelaren skickar en begäran till en annonsserver innehåller VAST/VMAP-svaret vanligtvis flera annonsskapare ( `MediaFile` -element) som vart och ett tillhandahåller en URL till en annan behållar-kodek-version. I vissa fall kan annonskreatörer i VAST/VMAP-svaret ge olika bithastighet för annonsen. Om du vill ange din egen prioritet och omformningsregler för dessa annonskreatörer kan du göra det i [!DNL AdobeTVSDKConfig.json] konfigurationsfil.

>[!IMPORTANT]
>
>* Ändra inte namnet på TVSDK-konfigurationsfilen. Namnet måste finnas kvar [!DNL AdobeTVSDKConfig.json].
>* Du kan montera den här filen var som helst som är tillgänglig för ditt paket.
>


Du kan ange två typer av regler i [!DNL AdobeTVSDKConfig.json]: *Prioritet* regler och *Normalisera* regler.

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
