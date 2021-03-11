---
description: SDK hämtar regelbundet listor över återkallade certifikat som publiceras av Adobe. Du måste se till att åtkomsten till de här filerna inte blockeras eller att kontrollen av dessa listor över återkallade certifikat inte förhindras.
title: Använda listor över återkallade certifikat som publicerats av Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Använda listor över återkallade certifikat som publicerats av Adobe{#consuming-crls-published-by-adobe}

SDK hämtar regelbundet listor över återkallade certifikat som publiceras av Adobe. Du måste se till att åtkomsten till de här filerna inte blockeras eller att kontrollen av dessa listor över återkallade certifikat inte förhindras.

SDK har ett konfigurationsalternativ som ignorerar fel när du hämtar Adobe-CRL:er, och du kan bara använda det här alternativet i utvecklingsmiljöer. I produktionsmiljöer måste licensservern hämta CRL:er från Adobe. Om licensservern inte kan hämta en giltig CRL har ett fel uppstått.
