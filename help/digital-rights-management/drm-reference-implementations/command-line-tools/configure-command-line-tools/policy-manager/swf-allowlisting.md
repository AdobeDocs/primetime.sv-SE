---
seo-title: Tillåt listning av SWF-program
title: Tillåt listning av SWF-program
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Tillåt listning av SWF-program{#swf-application-allowlisting}

Om du vill tillåta att ett SWF-program listas kan du göra något av följande:

* Du kan ange en URL till en SWF-fil. Detta är en mycket flexibel metod, särskilt i en utvecklingsmiljö där du regelbundet återskapar SWF-filen.
* Du kan ange en SWF-HASH. Detta är ett kryptografiskt sammandragsvärde för SWF-filen. Det här arbetssättet är mindre flexibelt (men mycket mer strikt) eftersom SWF HASH ändras när programmet ändras och återskapas. I den här situationen kommer allt innehåll som är bundet till föregående HASH inte att kunna spelas upp på den nya spelaren och måste paketeras om. Om du anger en [!DNL PolicyManager.jar] [!DNL .swf] fil beräknas hash-värdet automatiskt.

   Om du däremot använder Primetime DRM via Flash/Adobe Media Server (FMS/AMS) kan du ange sökvägen till dina specifika SWF-filer, och FMS/AMS kommer automatiskt att hash-koda SWF-filerna så att du kan infoga dem i DRM-principen som används för att paketera innehåll som direktuppspelas av FMS/AMS.

Mer information finns `policy.allowedSWFApplication.n` i *Konfigurationsegenskaper* .
