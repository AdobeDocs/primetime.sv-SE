---
title: Testa det packade innehållet
description: Testa det packade innehållet
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Testa det paketerade innehållet {#test-the-packaged-content}

Du bör verifiera att paketeringsåtgärden lyckades med hjälp av den allmänt tillgängliga Adobe Primetime Desktop Player (via Flash Player). Den här spelaren stöder bara HDS-innehåll. För att testa HLS-innehåll krävs en TSDK-aktiverad spelare i Primetime Browser.

1. Lägg innehållet på en webbserver.
1. Starta Primetimes DRM-spelare (tidigare Adobe Access) på https://drmtest2.adobe.com:8080/AccessPlayer/player.html.
1. Klistra in URL:en i HDS-manifestet ( [!DNL .f4m]) i spelarens navigeringsfält och klicka på knappen **[!UICONTROL Play]**.
