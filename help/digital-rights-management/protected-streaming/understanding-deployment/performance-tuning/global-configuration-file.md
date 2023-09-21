---
description: I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.
title: Global konfigurationsfil
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Prestandajustering {#performance-tuning}

I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.

## Global konfigurationsfil {#global-configuration-file}

Konfigurationsfilen innehåller följande inställningselement:

* `<Caching>` The `<Caching>` -element styr cachelagring av konfigurationsfiler i minnet. The `<Caching>` -elementet har stöd för följande syntax:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Styr hur ofta servern söker efter uppdateringar av konfigurationsfilerna. Ett lågt värde för `refreshDelaySeconds` påverkar prestandan negativt medan ett högre värde kan förbättra prestandan.

  Se *Konfigurationsfiler uppdateras* för mer information om `refreshDelaySeconds`.

* `numTenants` Anger antalet klientorganisationer. Ett värde som är lägre än antalet klientorganisationer påverkar prestandan eftersom begäranden till de återstående klienterna leder till cachemissar. Ett cacheminne för konfigurationsdata påverkar prestandan negativt. Därför rekommenderar vi att du anger det här värdet högre än antalet klientorganisationer som har konfigurerats för servern, såvida det inte finns minnesbegränsningar som du måste tänka på.

* `<Logging>` The `<Logging>` -elementet anger loggningsnivån och hur ofta loggfiler rullas. The `<Logging>` -elementet har stöd för följande syntax:

  ```
  <Logging level="..." rollingFrequency="..."/>
  ```

* `<level>`  `level` anger meddelanden i en logg. Värdet för `DEBUG` ger många loggmeddelanden, vilket kan påverka prestandan negativt. Vi rekommenderar att du använder en inställning på `WARN` för optimala prestanda. Det här värdet kan dock resultera i att viktig körningsinformation, som till exempel licensgranskningar, förloras. Om du vill spara logginformation med minimal prestandapåverkan måste du använda värdet `INFO`.

* `<rollingFrequency>`  `rollingFrequency` anger hur ofta loggfiler *rullad*. *`Rolling`* är en process som anger att en ny loggfil ska vara en aktiv logg. Den tidigare aktiva loggfilen kan därför inte längre ändras och anses därför vara *`rolled`*. Du kan ställa in rullningsintervallet till `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`, eller `NEVER`.

Se *Använda Adobe Primetime DRM SDK för att skydda innehåll* för tips om hur du optimerar prestanda.
