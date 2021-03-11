---
title: Prestandajustering
description: Prestandajustering
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Prestandajustering{#performance-tuning}

Använd följande tips för att förbättra prestandan:

* Att använda nätverks-HSM kan vara betydligt långsammare än att använda en direktansluten HSM.
* För bättre prestanda kan du som alternativ aktivera inbyggt stöd för kryptografiska åtgärder genom att distribuera de plattformsspecifika biblioteken i mappen [!DNL thirdparty/cryptoj] i SDK. Om du vill aktivera inbyggt stöd lägger du till biblioteket för din plattform (jsafe.dll för Windows eller libjsafe.so för Linux) i sökvägen.

   >[!NOTE]
   >
   >Om du kör flera webbprogram i samma Tomcat-instans och har `jsafe.dll` på sökvägen kan bara det första webbprogrammet som läser in `jsafe.dll`-biblioteket läsas in. Därför är det bara det första webbprogrammet som får det inbyggda stödet. Om du i så fall vill förbättra prestandan för alla webbprogram placerar du `cryptoj.jar`utanför WAR-filen. I katalogen `<tomcat_installation_folder>/lib`.

* Ett 64-bitars operativsystem, som 64-bitarsversionen av Red Hat® eller Windows, ger mycket bättre prestanda jämfört med ett 32-bitars operativsystem.

## Genererar slumptal (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Under vissa förhållanden kan Linux-miljöer pausa vid körning av DRM-relaterade åtgärder i Primetime som kräver slumpmässig nummergenerering, inklusive:

* Starta Adobe Primetime DRM-licensservern
* Principgenerering med verktyget [!DNL AdobePolicyManager]
* Paketera DRM-skyddat innehåll med Adobe Media Server eller Primetime OfflinePackager

Förseningar under dessa åtgärder beror ofta på en låg entropispool på Linux-servern.

I Linux genereras slumpmässiga tal från servermiljöns entropypool. Enropy-poolen underhålls normalt genom att maskinvaruavbrott tas emot av Linux-kärnan. Om en server är isolerad och inte får regelbundna indata från maskinvaruresurser (t.ex. en mus eller ett tangentbord) kan väntan på att återfylla entroppoolen utökas. I det här scenariot kan åtgärder som väntar på data från [!DNL /dev/random] pausa.

Du kan använda slumpmässiga generatorer för maskinvarubaserade nummer på Linux-servrar för att säkerställa att tillräcklig entropi genereras. Om det inte finns några slumpmässiga generatorer för maskinvaruantal i ett visst distributionsscenario kan du använda programvarubaserade lösningar för att öka uppdateringsfrekvensen för entropisolen. En sådan programvarulösning i Linux är [!DNL haveged] (HArdware Volatile Entropy Gatering and Expansion daemon).

## Identifierar tillgänglig Entropy {#section_686B311FE6144566B6939E9F20915ADC}

Kör följande kommando för att verifiera antalet bitar som är tillgängliga i en viss servers entropy-pool under en oväntad fördröjning:

```
cat /proc/sys/kernel/random/entropy_avail 
```

Ett felfritt Linux-system med mycket entropi kommer att returnera nästan 4 096 bitar entropi. Om det returnerade värdet är mindre än 200 är entropin väldigt lite.
