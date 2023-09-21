---
description: Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.
keywords: regler för kreativt urval;AdobeTVSDKConfig;ad creative priority;transformeringsregler
title: Uppdatera och skapa regler för urval
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Ökning {#update-ad-creative-selection-rules-overview}

Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.

När videospelaren skickar en begäran till en annonsserver innehåller VAST/VMAP-svaret vanligtvis flera annonsskapare ( `MediaFile` -element) som vart och ett tillhandahåller en URL till en annan behållar-kodek-version. I vissa fall kan annonskreatörer i VAST/VMAP-svaret ge olika bithastighet för annonsen. Om du vill ange din egen prioritet och omformningsregler för dessa annonskreatörer kan du göra det i [!DNL AdobeTVSDKConfig.json] konfigurationsfil.

>[!IMPORTANT]
>
>* Ändra inte namnet på TVSDK-konfigurationsfilen. Namnet måste finnas kvar [!DNL AdobeTVSDKConfig.json].
>* Den här filen måste placeras i [!DNL assets/] projektmapp.
>* Ljudspåret ändras inte om du ändrar ljudspår när annonsen spelas upp. En spelare bör inte tillåta användare att ändra ljudspåret när en annons spelas upp.
>

Du kan ange två typer av regler i [!DNL AdobeTVSDKConfig.json]: *Prioritet* regler och *Normalisera* regler.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Annonsreglerna anges med en JSON-fil. JSON-filens format ändras inte i båda versionerna av TVSDK. I TVSDK v3.0 måste dock JSON-filen för annonsregler finnas på en plats som är tillgänglig via en HTTP-URL. Programmet kan använda en instans av AuditudeSettings:

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
