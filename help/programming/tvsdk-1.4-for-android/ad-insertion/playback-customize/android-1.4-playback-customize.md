---
description: När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.
seo-description: När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.
seo-title: Anpassa uppspelning med annonser
title: Anpassa uppspelning med annonser
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Översikt {#customize-playback-with-ads-overview}

När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.

>[!TIP]
>
>Du kan åsidosätta standardbeteendet genom att använda `AdBreakPolicySelector` klassen.

Standardbeteendet varierar beroende på om användaren skickar annonsbrytningen under normal uppspelning eller genom att söka i en video eller flytta den med snabb fram- eller tillbakaspolning (tricks play).

Du kan anpassa beteendet för annonsuppspelning på följande sätt:

* Spara positionen där användaren slutade titta på videon och återuppta uppspelningen på samma plats i en framtida session.
* Om en annonsbrytning visas för användaren visar du inga ytterligare annonser under ett antal minuter, även om användaren söker efter en ny position.
* Om innehållet inte kan spelas upp efter några minuter startar du om strömmen eller växlar om till en annan källa för samma innehåll.

   För att användaren ska kunna hoppa över annonser och återuppta den tidigare misslyckade positionen kan du inaktivera pre-roll- och/eller middle-roll-annonser under redundansuppspelningssessionen. TVSDK tillhandahåller metoder för att aktivera hoppning av annonser före och efter rullning.