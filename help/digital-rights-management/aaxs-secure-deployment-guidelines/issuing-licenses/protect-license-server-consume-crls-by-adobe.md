---
seo-title: Förbruka listor över återkallade certifikat som publicerats av Adobe
title: Förbruka listor över återkallade certifikat som publicerats av Adobe
uuid: 43f65edb-0c96-46ab-b787-1b5f0b4b093e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Förbruka listor över återkallade certifikat som publicerats av Adobe{#consume-crls-published-by-adobe}

SDK hämtar regelbundet listor över återkallade certifikat som publicerats av Adobe. Blockera inte åtkomst till dessa filer och förhindra inte att dessa listor över återkallade certifikat verkställs.

SDK har ett konfigurationsalternativ som ignorerar fel när Adobe-CRL:er hämtas. Det här alternativet får endast användas i utvecklingsmiljöer. I produktionsmiljöer måste licensservern kunna hämta listor över återkallade certifikat från Adobe. Det gick inte att hämta en giltig CRL.
