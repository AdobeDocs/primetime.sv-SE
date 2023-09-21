---
title: SWF-programmet tillåter listning
description: SWF-programmet tillåter listning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# SWF-programmet tillåter listning {#swf-application-allowlisting}

Om du vill använda tillåtelselista som SWF kan du följa någon av dessa två strategier:

* Du kan ange en URL till en SWF. Detta är en mycket flexibel strategi, särskilt i en utvecklingsmiljö där du regelbundet återuppbygger SWF.
* Du kan ange SWF HASH. Det här är ett kryptografiskt sammandragsvärde för SWF. Detta tillvägagångssätt är mindre flexibelt (men mycket mer strikt) eftersom SWF HASH kommer att ändras när programmet ändras och återskapas. I den här situationen kommer allt innehåll som är bundet till föregående HASH inte att kunna spelas upp på den nya spelaren och måste paketeras om. The [!DNL PolicyManager.jar] funktionen beräknar hashen automatiskt om du anger en [!DNL .swf] -fil.

  Om du däremot använder Primetime DRM via Flash/Adobe Media Server (FMS/AMS) kan du ange sökvägen till dina SWF, och FMS/AMS kommer automatiskt att hash-koda SWF så att du kan infoga den i DRM-principen som används för att paketera innehåll som direktuppspelas av FMS/AMS.

Se `policy.allowedSWFApplication.n` in *Konfigurationsegenskaper* för mer information.
