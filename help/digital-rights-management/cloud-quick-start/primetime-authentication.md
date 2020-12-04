---
seo-title: Adobe Primetime-autentisering (valfritt)
title: Adobe Primetime-autentisering (valfritt)
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Adobe Primetime-autentisering (valfritt) {#adobe-primetime-authentication-optional}

Om DRM-principen som används för att paketera innehållet är en anonym princip, kommer en licens att utfärdas för alla licensbegäranden. Primetime Cloud DRM har också stöd för autentisering via Adobe Primetime-autentisering. Om den här funktionen är aktiverad utfärdas ingen licens såvida inte klientenheten först har skaffat en Primetime-autentiseringstoken och ställt in den lokalt via lämpligt klient-API ( `setAuthenticationToken`) för inställning av anpassade autentiseringstoken. Mer information om hur du integrerar Primetime-autentisering i ditt autentiseringsarbetsflöde finns i: [Adobe Primetime-autentisering.](https://tve.helpdocsonline.com/home)

Om DRM-principen anger att autentisering med Pri-metime krävs vid licensköp, tolkas och valideras den korta medietoken för Primetime-autentisering. Om DRM-principen anger `ResourceID` eller `RequestorID` validerar licensservern även token mot dessa egenskaper. Om de inte anges anger licensservern egenskapen/egenskaperna som&quot;null&quot; under tokenvalidering. Endast om tokenvalideringen lyckas utfärdas en licens. I annat fall skickas en 3328 DRMErrorEvent med en 305-felkod (User Not Authorized) av klienten.

Primetimes autentiseringsparametrar måste anges i den princip som används för att paketera innehållet som ska kräva Primetime-autentisering.

De relevanta egenskaperna är:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>När du använder Primetime-autentisering i samband med (DRM) licensrotationsfunktionen bör du tänka på att Primetime-autentiseringen med kort medietoken (SMT) har ett kort giltighetsdatum. Om ditt program planerar att använda licensrotation (t.ex. för att stödja *Utpressningar*) måste programmet vara medvetet om detta och uppdatera dess korta medietoken för autentisering av primär tid innan licensen roteras.