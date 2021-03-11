---
title: Global konfigurationsfil
description: Global konfigurationsfil
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Global konfigurationsfil{#global-configuration-file}

Den största prestandapåverkan du kan göra är att använda inställningarna i den globala konfigurationsfilen flashaccess-global.xml. Dessa inställningar inkluderar elementen `<Caching>` och `<Logging>`.

* `<Caching>` Elementet  `<Caching>` styr cachelagring av konfigurationsfiler i minnet. `<Caching>`-elementet har följande syntax:

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` styr hur ofta servern söker efter uppdateringar av konfigurationsfilerna. Ett lågt värde för `refreshDelaySeconds` påverkar prestandan negativt, medan ett högre värde kan förbättra prestandan. Mer information om `refreshDelaySeconds` finns i &quot;[Uppdatera konfigurationsfiler](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)&quot;.

   * `numTenants` Anger antalet klientorganisationer. Ett värde som är lägre än antalet klientorganisationer påverkar troligtvis prestandan eftersom begäranden till de återstående klienterna leder till cachemissar. Ett cacheminne för konfigurationsdata påverkar prestandan negativt. Därför rekommenderar Adobe att du anger det här värdet som högre än antalet klientorganisationer som konfigurerats för servern, såvida det inte finns minnesbegränsningar att tänka på.

* `<Logging>` Elementet  `<Logging>` anger loggningsnivån och hur ofta loggfiler rullas. `<Logging>`-elementet har följande syntax:

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` anger vilka meddelanden som ska loggas. Värdet &quot;DEBUG&quot; ger många loggmeddelanden och kan påverka prestandan negativt. Adobe rekommenderar att du anger &quot;WARN&quot; för optimala prestanda. Detta värde riskerar dock att förlora viktig körningsinformation, som till exempel licensrevisioner. Använd värdet INFO om du vill bevara värdefull logginformation med minimal inverkan på prestandan.
   * `rollingFrequency` anger hur ofta loggfiler  *rullas*. Rullande är den process där en ny loggfil blir aktiv logg, medan den tidigare aktiva loggfilen inte längre skrivs till och betraktas som rullande. Rullningsintervallet kan anges till MINUTELY, HOURLY, TWICE-DAILY, DAILY, WEEKLY, MONTHLY eller NEVER.

Mer information om hur du optimerar prestanda finns i *Använda Adobe Access SDK för att skydda innehåll*.
