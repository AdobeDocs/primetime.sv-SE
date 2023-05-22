---
title: Prestandajustering
description: Prestandajustering
copied-description: true
exl-id: f6b2338e-a209-4881-a599-ded5f1498daf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Prestandajustering{#performance-tuning}

Använd följande tips för att förbättra prestandan:

* Att använda nätverks-HSM kan vara betydligt långsammare än att använda en direktansluten HSM.
* För bättre prestanda kan du som tillval aktivera inbyggt stöd för kryptografiska åtgärder genom att distribuera de plattformsspecifika biblioteken i mappen&quot;Third party/cryptoj&quot; i SDK. Om du vill aktivera inbyggt stöd lägger du till biblioteket för din plattform (jsafe.dll för Windows eller libjsafe.so för Linux) i sökvägen.

   >[!NOTE]
   >
   >Om du kör flera webbprogram i samma Tomcat-instans och har `jsafe.dll` på sökvägen är det bara det första webbprogrammet som läser in som kan läsa in `jsafe.dll` bibliotek. Därför är det bara det första webbprogrammet som får det inbyggda stödet. Om du i så fall vill förbättra prestandan för alla webbprogram ska du montera `cryptoj.jar`utanför WAR-filen. I `<tomcat_installation_folder>/lib` katalog.

* Ett 64-bitars operativsystem, som 64-bitarsversionen av Red Hat® eller Windows, ger mycket bättre prestanda jämfört med ett 32-bitars operativsystem.
