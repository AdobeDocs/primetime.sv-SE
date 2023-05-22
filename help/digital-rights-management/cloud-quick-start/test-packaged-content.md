---
title: Testa det packade innehållet
description: Testa det packade innehållet
copied-description: true
exl-id: 98456bf8-5d4d-47a7-905a-e6dac1e826ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Testa det packade innehållet {#test-the-packaged-content}

Du bör verifiera att paketeringsåtgärden lyckades med hjälp av den allmänt tillgängliga Adobe Primetime Desktop Player (via Flash Player). Den här spelaren stöder bara HDS-innehåll. För att testa HLS-innehåll krävs en TSDK-aktiverad spelare i Primetime Browser.

1. Lägg innehållet på en webbserver.
1. Starta Primetimes DRM-spelare (tidigare Adobe Access) på https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Klistra in URL:en i HDS-manifestet ( [!DNL .f4m]) till spelarens navigeringsfält och klicka på **[!UICONTROL Play]** -knappen.
