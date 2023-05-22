---
title: Förbruka listor över återkallade certifikat som publicerats av Adobe
description: Förbruka listor över återkallade certifikat som publicerats av Adobe
copied-description: true
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Förbruka listor över återkallade certifikat som publicerats av Adobe{#consume-crls-published-by-adobe}

SDK hämtar regelbundet listor över återkallade certifikat som publicerats av Adobe. Blockera inte åtkomst till dessa filer och förhindra inte att dessa listor över återkallade certifikat verkställs.

SDK har ett konfigurationsalternativ som ignorerar fel när Adobe-CRL:er hämtas. Det här alternativet får endast användas i utvecklingsmiljöer. I produktionsmiljöer måste licensservern kunna hämta listor över återkallade certifikat från Adobe. Det gick inte att hämta en giltig CRL.
