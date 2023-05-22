---
description: När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.
title: Anpassa uppspelning med annonser
exl-id: 3e945113-f44f-4b53-b952-10307f8d2d2f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Översikt {#customize-playback-with-ads-overview}

När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.

>[!TIP]
>
>Du kan åsidosätta standardbeteendet med `AdBreakPolicySelector` klassen.

Standardbeteendet varierar beroende på om användaren skickar annonsbrytningen under normal uppspelning eller genom att söka i en video eller flytta den med snabb fram- eller tillbakaspolning (tricks play).

Du kan anpassa beteendet för annonsuppspelning på följande sätt:

* Spara positionen där användaren slutade titta på videon och återuppta uppspelningen på samma plats i en framtida session.
* Om en annonsbrytning visas för användaren visar du inga ytterligare annonser under ett antal minuter, även om användaren söker efter en ny position.
* Om innehållet inte kan spelas upp efter några minuter startar du om strömmen eller växlar om till en annan källa för samma innehåll.

   För att användaren ska kunna hoppa över annonser och återuppta den tidigare misslyckade positionen kan du inaktivera annonser före och/eller meddelanden i mellanrullning under redundansuppspelningssessionen. TVSDK tillhandahåller metoder för att aktivera hoppning av annonser före och efter rullning.
