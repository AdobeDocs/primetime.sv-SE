---
description: I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.
seo-description: I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.
seo-title: Global konfigurationsfil
title: Global konfigurationsfil
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Prestandajustering {#performance-tuning}

I det här avsnittet beskrivs prestandarelaterade överväganden. Eventuella inställningar i den globala konfigurationsfilen som kallas flashaccess-global.xml påverkar prestandan.

## Global konfigurationsfil {#global-configuration-file}

Konfigurationsfilen innehåller följande inställningselement:

* `<Caching>` Elementet styr `<Caching>` cachelagring av konfigurationsfiler i minnet. Elementet `<Caching>` har stöd för följande syntax:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Styr hur ofta servern söker efter uppdateringar av konfigurationsfilerna. Ett lågt värde för påverkar prestandan `refreshDelaySeconds` negativt medan ett högre värde kan förbättra prestandan.

   Mer information om *konfigurationsfiler* finns i Uppdatera `refreshDelaySeconds`.

* `numTenants` Anger antalet klientorganisationer. Ett värde som är lägre än antalet klientorganisationer påverkar prestandan eftersom begäranden till de återstående klienterna leder till cachemissar. Ett cacheminne för konfigurationsdata påverkar prestandan negativt. Därför rekommenderar vi att du anger det här värdet högre än antalet klientorganisationer som har konfigurerats för servern, såvida det inte finns minnesbegränsningar som du måste tänka på.

* `<Logging>` Elementet anger `<Logging>` loggningsnivån och med vilken frekvens loggfilerna rullas. Elementet `<Logging>` har stöd för följande syntax:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  anger meddelanden `level` till en logg. Värdet `DEBUG` ger många loggmeddelanden, vilket kan påverka prestandan negativt. Vi rekommenderar att du använder en inställning på `WARN` för optimala prestanda. Det här värdet kan dock resultera i att viktig körningsinformation, som till exempel licensgranskningar, förloras. Om du vill spara logginformation med minimal prestandapåverkan måste du använda värdet `INFO`.

* `<rollingFrequency>`  `rollingFrequency` anger hur ofta loggfiler *rullas*. *`Rolling`* är en process som anger att en ny loggfil ska vara en aktiv logg. Den tidigare aktiva loggfilen kan därför inte längre ändras och kommer att användas *`rolled`*. Du kan ange att rullande intervall ska vara `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`eller `NEVER`.

Se *Använda Adobe Primetime DRM SDK för att skydda innehåll* för tips om hur du optimerar prestanda.