---
description: Du kan spåra videoanvändningen i implementeringen av Android-referensen i Primetime genom att konfigurera den så att den fungerar med ditt Adobe Analytics-konto.
seo-description: Du kan spåra videoanvändningen i implementeringen av Android-referensen i Primetime genom att konfigurera den så att den fungerar med ditt Adobe Analytics-konto.
seo-title: Konfigurera videoanalys
title: Konfigurera videoanalys
uuid: ce2ebab3-b3c8-472a-9c54-16ddb1c3cc4e
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Konfigurera videoanalys {#configure-video-analytics}

Du kan spåra videoanvändningen i implementeringen av Android-referensen i Primetime genom att konfigurera den så att den fungerar med ditt Adobe Analytics-konto. Referensimplementeringen av Android är utformad för att skicka videoanvändning och pulsslagdata till Adobe Analytics. Om du vill aktivera den här funktionen måste du först kontakta din Adobe Primetime-representant och skapa ett Adobe Analytics-konto.

Referensimplementeringen har två platser som du måste konfigurera för att kunna integrera Adobe Analytics. Konfigurationerna för videoanalys vid körning börjar gälla när en ny video har valts för uppspelning (dvs. när en ny PlayerActivity har skapats).

1. Konfigurera alternativ för inläsning i `ADBMobileConfig.json` resursfilen.

   Den här filen tillhandahålls av din Adobe-representant. Det ingår inte i Primetime SDK-paketet som standard. Mer information om inställningarna i den här konfigurationsfilen finns i Android Programmer&#39;s Guide här: Initiera och konfigurera videoanalyser.
1. Konfigurera körningsalternativ på menyn Inställningar för referensimplementering

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Körningsalternativ | Beskrivning |
   |---|---|
   | Spårningsserver för videoanalys | URL för videoanalysens back-end-samlingens slutpunkt. Här skickas alla anrop till spårning av pulsslag. |
   | Jobb-ID | Bearbetningsjobbets identifierare. Detta anger för den bakre slutpunkten vilken typ av bearbetning som ska användas för videospårningsanrop. |
   | Kanal | Namnet på den kanal där användaren tittar på innehållet. För mobilprogram är det vanligtvis programmets namn. |
   | Utgivare | Namnet på innehållsutgivaren |
   | Felsökningsloggning | Aktiverar omfattande loggning. Inaktiverat som standard kan detta påverka prestanda när det är aktiverat, så du inaktiverar detta för en produktionsmiljö. |
   | Tyst läge | När detta är aktiverat görs inga nätverksanrop, vilket är användbart för lokal felsökning, men måste inaktiveras för en produktionsmiljö. |