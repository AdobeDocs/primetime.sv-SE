---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

    * Om du implementerar din egen &quot;AdvertisingFactory&quot;-klass returnerar du null för &quot;createAdPolicySelector&quot;.
    
    * Om du inte har någon anpassad implementering för klassen AdvertisingFactory använder TVSDK en standardväljare för annonspolicy.
