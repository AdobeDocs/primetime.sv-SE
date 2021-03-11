---
title: SWF-program tillåter listning
description: SWF-program tillåter listning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# SWF-programmet tillåter listning {#swf-application-allowlisting}

Om du vill använda tillåtelselista som SWF-program kan du göra något av följande:

* Du kan ange en URL till en SWF-fil. Detta är en mycket flexibel metod, särskilt i en utvecklingsmiljö där du regelbundet återskapar SWF-filen.
* Du kan ange en SWF-HASH. Detta är ett kryptografiskt sammandragsvärde för SWF-filen. Det här arbetssättet är mindre flexibelt (men mycket mer strikt) eftersom SWF HASH ändras när programmet ändras och återskapas. I den här situationen kommer allt innehåll som är bundet till föregående HASH inte att kunna spelas upp på den nya spelaren och måste paketeras om. Verktyget [!DNL PolicyManager.jar] beräknar hashen automatiskt om du anger en [!DNL .swf]-fil.

   Om du däremot använder Primetime DRM via Flash/Adobe Media Server (FMS/AMS) kan du ange sökvägen till dina specifika SWF-filer, och FMS/AMS kommer automatiskt att hash-koda SWF-filerna så att du kan infoga dem i DRM-principen som används för att paketera innehåll som direktuppspelas av FMS/AMS.

Mer information finns i `policy.allowedSWFApplication.n` i *Konfigurationsegenskaper*.
