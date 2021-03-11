---
title: Förbruka listor över återkallade certifikat som publicerats av Adobe
description: Förbruka listor över återkallade certifikat som publicerats av Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Förbruka listor över återkallade certifikat som publicerats av Adobe{#consume-crls-published-by-adobe}

SDK hämtar regelbundet listor över återkallade certifikat som publicerats av Adobe. Blockera inte åtkomst till dessa filer och förhindra inte att dessa listor över återkallade certifikat verkställs.

SDK har ett konfigurationsalternativ som ignorerar fel när Adobe-CRL:er hämtas. Det här alternativet får endast användas i utvecklingsmiljöer. I produktionsmiljöer måste licensservern kunna hämta listor över återkallade certifikat från Adobe. Det gick inte att hämta en giltig CRL.
