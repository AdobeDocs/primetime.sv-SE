---
description: Du kan välja att använda standardbeteenden för annonser.
title: Använd standardbeteendet för uppspelning
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Använd standardbeteendet för uppspelning {#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

    * Om du implementerar din egen &quot;AdvertisingFactory&quot;-klass returnerar du null för &quot;createAdPolicySelector&quot;.
    
    * Om du inte har någon anpassad implementering för klassen AdvertisingFactory använder TVSDK en standardväljare för annonspolicy.
