---
seo-title: Prestandajustering
title: Prestandajustering
uuid: bb5321a0-48ef-49cb-aaf0-00d7ab9562fe
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
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
   >Om du kör flera webbprogram i samma Tomcat-instans och har `jsafe.dll` på sökvägen kan bara det första webbprogrammet som läser in `jsafe.dll` biblioteket läsas in. Därför är det bara det första webbprogrammet som får det inbyggda stödet. Om du i så fall vill förbättra prestandan för alla webbprogram placerar du `cryptoj.jar`utanför WAR-filen. Till exempel i `<tomcat_installation_folder>/lib` katalogen.

* Ett 64-bitars operativsystem, som 64-bitarsversionen av Red Hat® eller Windows, ger mycket bättre prestanda jämfört med ett 32-bitars operativsystem.

