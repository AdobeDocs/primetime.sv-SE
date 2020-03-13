---
description: När TVSDK påträffar en trasig VMAP i ett annonsserversvar skickas ett 1109-fel (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: När TVSDK påträffar en trasig VMAP i ett annonsserversvar skickas ett 1109-fel (NETWORK_AD_URL_FAILED).
seo-title: Klientfelhantering för trasig VMAP
title: Klientfelhantering för trasig VMAP
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Klientfelhantering för trasig VMAP {#client-error-handling-for-broken-vmap}

När TVSDK påträffar en trasig VMAP i ett annonsserversvar skickas ett 1109-fel (NETWORK_AD_URL_FAILED).

Beroende på vilken typ av annonsserversvar det är, och på dina inställningar för annonsinläsning, kan spelaren få olika antal 1109-fel när TVSDK stöter på en trasig VMAP i ett annonsserversvar.

Låt oss titta på ett scenario där annonsserverns svar pekar på VMAP XML. Låt oss också säga att annonsserverns svar har fyra tillgängliga annonsplatser, där var och en pekar på samma VMAP. Slutligen, låt oss säga att denna VMAP är trasig.

I det här scenariot, om lazy ad ad annonsupplösning är aktiverat ([Aktivera lat annonsmatchning](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), skickar TVSDK två 1 109-fel (inte ett som kan förväntas): ett fel skickas vid varje tolkningspass över tidslinjen. Detta beror på att TVSDK tolkar annonserna på två omgångar när lat annonslösande är aktiverat: den första omgången inträffar precis innan innehållsuppspelningen startar för pre-roll-ads, och den andra omgången inträffar efter att uppspelningen startar, för annonser i mellanrullning och post-roll.

>[!NOTE]
>
>Om du inaktiverar lat och löst kommer TVSDK endast att utlösa ett 1109-fel (endast ett tolkningspass).