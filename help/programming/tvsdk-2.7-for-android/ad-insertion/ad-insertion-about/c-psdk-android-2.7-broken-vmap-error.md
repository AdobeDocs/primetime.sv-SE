---
description: När TVSDK påträffar en trasig VMAP i ett annonsserversvar skickas ett 1109-fel (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: När TVSDK påträffar en trasig VMAP i ett annonsserversvar skickas ett 1109-fel (NETWORK_AD_URL_FAILED).
seo-title: Klientfelhantering för trasig VMAP
title: Klientfelhantering för trasig VMAP
uuid: 7cc68c86-bb49-4a1b-a1ec-65ca4c94d75d
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Klientfelhantering för trasig VMAP {#client-error-handling-for-broken-vmap}

När TVSDK påträffar en trasig VMAP i ett annonsserversvar skickas ett 1109-fel (NETWORK_AD_URL_FAILED).

Beroende på vilken typ av annonsserversvar det är, och på dina inställningar för annonsinläsning, kan spelaren få olika antal 1109-fel när TVSDK stöter på en trasig VMAP i ett annonsserversvar.

Låt oss titta på ett scenario där annonsserverns svar pekar på VMAP XML. Låt oss också säga att annonsserverns svar har fyra tillgängliga annonsplatser, där var och en pekar på samma VMAP. Slutligen, låt oss säga att denna VMAP är trasig.

I det här scenariot, om lazy ad ad annonsupplösning är aktiverad ( [Aktivera lat och lösa](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md)), skickar TVSDK två 1109-fel (inte ett som kan förväntas): ett fel skickas vid varje tolkningspass över tidslinjen. Detta beror på att TVSDK tolkar annonserna på två omgångar när lat annonslösande är aktiverat: den första omgången inträffar precis innan innehållsuppspelningen startar för pre-roll-ads, och den andra omgången inträffar efter att uppspelningen startar, för annonser i mellanrullning och post-roll.

>[!NOTE]
>
>Om du inaktiverar lat och löst kommer TVSDK endast att utlösa ett 1109-fel (endast ett tolkningspass).

