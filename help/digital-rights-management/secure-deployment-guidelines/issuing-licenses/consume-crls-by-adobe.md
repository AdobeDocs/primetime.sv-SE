---
description: SDK hämtar regelbundet listor över återkallade certifikat som publiceras av Adobe. Du måste se till att åtkomsten till de här filerna inte blockeras eller att kontrollen av dessa listor över återkallade certifikat inte förhindras.
seo-description: SDK hämtar regelbundet listor över återkallade certifikat som publiceras av Adobe. Du måste se till att åtkomsten till de här filerna inte blockeras eller att kontrollen av dessa listor över återkallade certifikat inte förhindras.
seo-title: Använda listor över återkallade certifikat som publicerats av Adobe
title: Använda listor över återkallade certifikat som publicerats av Adobe
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Använda listor över återkallade certifikat som publicerats av Adobe{#consuming-crls-published-by-adobe}

SDK hämtar regelbundet listor över återkallade certifikat som publiceras av Adobe. Du måste se till att åtkomsten till de här filerna inte blockeras eller att kontrollen av dessa listor över återkallade certifikat inte förhindras.

SDK har ett konfigurationsalternativ som ignorerar fel när du hämtar Adobe-CRL:er, och du kan bara använda det här alternativet i utvecklingsmiljöer. I produktionsmiljöer måste licensservern hämta CRL:er från Adobe. Om licensservern inte kan hämta en giltig CRL har ett fel uppstått.
