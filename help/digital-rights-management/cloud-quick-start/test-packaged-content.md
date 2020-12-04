---
seo-title: Testa det packade innehållet
title: Testa det packade innehållet
uuid: 99df417a-85ce-45da-bfcf-33df2197bf5b
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Testa det paketerade innehållet {#test-the-packaged-content}

Du bör verifiera att paketeringsåtgärden lyckades med hjälp av den allmänt tillgängliga Adobe Primetime Desktop Player (via Flash Player). Den här spelaren stöder bara HDS-innehåll. För att testa HLS-innehåll krävs en TSDK-aktiverad spelare i Primetime Browser.

1. Lägg innehållet på en webbserver.
1. Starta Primetimes DRM-spelare (tidigare Adobe Access) på https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Klistra in URL:en i HDS-manifestet ( [!DNL .f4m]) i spelarens navigeringsfält och klicka på knappen **[!UICONTROL Play]**.
