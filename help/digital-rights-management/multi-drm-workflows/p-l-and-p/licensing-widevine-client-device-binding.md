---
description: I vissa fall kanske du vill hindra slutanvändare från att spela upp innehåll på flera enheter när innehållet köpts eller hyrts. Om kunden använder Expressplay kan detta göras genom att använda Expressplay-API:erna för att binda användarens Expressplay-token till användarens dator.
title: Enhetsbindning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Enhetsbindning{#device-binding}

I vissa fall kanske du vill hindra slutanvändare från att spela upp innehåll på flera enheter när innehållet köpts eller hyrts. Om kunden använder Expressplay kan detta göras genom att använda Expressplay-API:erna för att binda användarens Expressplay-token till användarens dator.

Du kan använda API:erna på följande sätt.

1. Generera en cookie.
1. Skicka en begäran om att skapa en dummy-token med den genererade cookien som antingen är bifogad som en frågesträng (cookie=`<cookie>`) eller som rubriker.
1. Låt användarens dator skicka en licensbegäran till Expresshow-licensservern med hjälp av ovanstående token, till exempel genom att spela upp ett dummy-innehåll.

   När den här dummy-licensbegäran lyckas associerar den användarens device_id (beräknad eller genererad av DRM-implementeringen på användarens enhet) med cookien i Expressplay back-end. Denna cookie används sedan på följande sätt:

   * Vid köp/hyra av innehåll skickar koden en fråga till uttryckets back-end för användarens device_id genom att skicka den associerade cookien ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Skicka en begäran om generering av token med det köpta innehållets nyckel (CEK), keyID (CEKSID), principer och annan information, och bifoga cookien och device_id ovan som `cookie` korrelationsparameter och `deviceid` parameter för tokenbegränsning.

   * Ange denna token för användaren.

     Den här processen genererar en token för innehållet som är bundet till användarens device_id. När användarens dator skickar en licensbegäran med denna token, kommer Expressplay back-end att kontrollera token&#39;s device_id med licensbegärans device_id.

     En exempeltillståndsserver för uttryck implementerar det här arbetsflödet.
