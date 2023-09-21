---
description: Du kan spåra videoanvändningen i implementeringen av Android-referensen i Primetime genom att konfigurera den så att den fungerar med ditt Adobe Analytics-konto.
title: Konfigurera videoanalys
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Konfigurera videoanalys {#configure-video-analytics}

Du kan spåra videoanvändningen i implementeringen av Android-referensen i Primetime genom att konfigurera den så att den fungerar med ditt Adobe Analytics-konto. Referensimplementeringen av Android är utformad för att skicka videoanvändning och pulsslagdata till Adobe Analytics. Om du vill aktivera den här funktionen måste du först kontakta Adobe Primetime och skapa ett Adobe Analytics-konto.

Referensimplementeringen har två platser som du måste konfigurera för att aktivera Adobe Analytics-integreringen. Konfigurationerna för videoanalys vid körning börjar gälla när en ny video har valts för uppspelning (dvs. när en ny PlayerActivity har skapats).

1. Konfigurera alternativ för inläsningstid i dialogrutan `ADBMobileConfig.json` resursfil.

   Den här filen tillhandahålls av din Adobe-representant. Det ingår inte i Primetime SDK-paketet som standard. Mer information om inställningarna i den här konfigurationsfilen finns i Android Programmer&#39;s Guide här: Initialize and configure video analytics.
1. Konfigurera körningsalternativ på inställningsmenyn för referensimplementering

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | Körningsalternativ | Beskrivning |
   |---|---|
   | Spårningsserver för videoanalys | URL för videoanalysens back-end-samlingens slutpunkt. Här skickas alla anrop till spårning av pulsslag. |
   | Jobb-ID | Bearbetningsjobbets identifierare. Detta anger för den bakre slutpunkten vilken typ av bearbetning som ska användas för videospårningsanrop. |
   | Kanal | Namnet på den kanal där användaren tittar på innehållet. För mobilprogram är det vanligtvis programmets namn. |
   | Utgivare | Namnet på innehållsutgivaren |
   | Felsökningsloggning | Aktiverar omfattande loggning. Inaktiverat som standard kan detta påverka prestanda när det är aktiverat, så du inaktiverar detta för en produktionsmiljö. |
   | Tyst läge | När detta är aktiverat görs inga nätverksanrop, vilket är användbart för lokal felsökning, men det måste inaktiveras för en produktionsmiljö. |
