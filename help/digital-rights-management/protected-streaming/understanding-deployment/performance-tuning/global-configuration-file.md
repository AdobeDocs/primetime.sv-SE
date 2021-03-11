---
description: I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.
title: Global konfigurationsfil
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Prestandajustering {#performance-tuning}

I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.

## Global konfigurationsfil {#global-configuration-file}

Konfigurationsfilen innehåller följande inställningselement:

* `<Caching>` Elementet  `<Caching>` styr cachelagring av konfigurationsfiler i minnet. `<Caching>`-elementet stöder följande syntax:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Styr hur ofta servern söker efter uppdateringar av konfigurationsfilerna. Ett lågt värde för `refreshDelaySeconds` påverkar prestandan negativt medan ett högre värde kan förbättra prestandan.

   Mer information om `refreshDelaySeconds` finns i *Uppdatera konfigurationsfiler*.

* `numTenants` Anger antalet klientorganisationer. Ett värde som är lägre än antalet klientorganisationer påverkar prestandan eftersom begäranden till de återstående klienterna leder till cachemissar. Ett cacheminne för konfigurationsdata påverkar prestandan negativt. Därför rekommenderar vi att du anger det här värdet högre än antalet klientorganisationer som har konfigurerats för servern, såvida det inte finns minnesbegränsningar som du måste tänka på.

* `<Logging>` Elementet  `<Logging>` anger loggningsnivån och hur ofta loggfiler rullas. `<Logging>`-elementet stöder följande syntax:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` anger meddelanden i en logg. Värdet `DEBUG` ger många loggmeddelanden, vilket kan påverka prestandan negativt. Vi rekommenderar att du använder inställningen `WARN` för optimala prestanda. Det här värdet kan dock resultera i att viktig körningsinformation, som till exempel licensgranskningar, förloras. Om du vill spara logginformation med minimal prestandapåverkan måste du använda värdet `INFO`.

* `<rollingFrequency>`  `rollingFrequency` anger hur ofta loggfiler  *rullas*. *`Rolling`* är en process som anger att en ny loggfil ska vara en aktiv logg. Den tidigare aktiva loggfilen kan därför inte längre ändras och anses vara *`rolled`*. Du kan ange rullande intervall till `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY` eller `NEVER`.

Tips om hur du optimerar prestanda finns i *Använda Adobe Primetime DRM SDK för att skydda innehåll*.