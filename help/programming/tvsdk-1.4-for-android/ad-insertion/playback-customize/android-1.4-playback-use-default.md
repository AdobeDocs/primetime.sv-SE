---
description: Du kan välja att använda standardbeteenden för annonser.
seo-description: Du kan välja att använda standardbeteenden för annonser.
seo-title: Använd standardbeteendet för uppspelning
title: Använd standardbeteendet för uppspelning
uuid: ccda5223-17c1-4cda-b875-e706f5dc8648
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

    * Om du implementerar din egen &quot;AdvertisingFactory&quot;-klass returnerar du null för &quot;createAdPolicySelector&quot;.
    
    * Om du inte har någon anpassad implementering för klassen AdvertisingFactory använder TVSDK en standardväljare för annonspolicy.