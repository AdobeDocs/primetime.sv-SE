---
description: Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.
title: Uppdatera och skapa regler för urval
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Översikt {#updating-ad-creative-selection-rules}

Du kan använda TVSDK-konfigurationsfilen (AdobeTVSDKConfig.json) för att uppdatera prioriteterna för annonsmarkering på VAST-/VMAP-svar. Du kan också använda den här konfigurationsfilen för att definiera URL-transformeringsreglerna för källa för annonskreatörer.

När videospelaren skickar en begäran till en annonsserver innehåller VAST/VMAP-svaret vanligtvis flera annonsskapare ( `MediaFile`-element), som var och en tillhandahåller en URL till en annan behållar-kodekversion. I vissa fall kan annonskreatörer i VAST/VMAP-svaret ge olika bithastighet för annonsen. Om du vill ange din egen prioritet och omformningsregler för dessa annonskreatörer kan du göra det i konfigurationsfilen [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Ändra inte namnet på TVSDK-konfigurationsfilen. Namnet måste vara kvar [!DNL AdobeTVSDKConfig.json].
>* Den här filen bör finnas på ditt leveransnätverk (CDN).

>



Du kan ange två typer av regler i [!DNL AdobeTVSDKConfig.json]: *Prioritet*-regler och *Normalisera*-regler.
