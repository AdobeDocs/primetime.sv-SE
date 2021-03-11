---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

    * Om du implementerar din egen &quot;AdvertisingFactory&quot;-klass returnerar du null för &quot;createAdPolicySelector&quot;.
    
    * Om du inte har någon anpassad implementering för klassen AdvertisingFactory använder TVSDK en standardväljare för annonspolicy.