---
seo-title: Övervakning
title: Övervakning
uuid: ee62c55f-0d44-40f4-a2c7-39456f4d3d99
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Övervakning{#monitoring}

Individualiseringsservern och nyckelgenereringsservern har båda en statussida, som du kan använda för att fastställa serverarnas hälsa.

* **Sida för personaliseringsstatus:** [!DNL https://SERVER:PORT/flashaccess/status]

   * Rapporterar&quot;live&quot; om appservern körs och appen kan göra en GET-förfrågan till nyckelgenereringsservern
   * Sidan rapporterar &quot;Alive&quot; eller ingenting. Ingen information om programmet visas, så den här sidan kan användas för övervakning utanför brandväggen.

* **Statussida för nyckelgenerering:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * Rapporterar&quot;Alive&quot; om programservern körs
   * Alla nyckelgenererings-URL:er får bara vara tillgängliga internt

* **Sida för personaliseringsstatistik:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * Inkluderar statistik om Individualization-servern, t.ex. antalet begäranden som hanteras och antalet nycklar som finns i cachen
   * Den här sidan får endast vara åtkomlig internt

* **Statistik för nyckelgenerering:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * Inkluderar statistik om nyckelgenereringsservern, t.ex. antalet begäranden som hanteras och antalet nyckelfiler som finns tillgängliga på disken
   * Alla nyckelgenererings-URL:er får bara vara tillgängliga internt

