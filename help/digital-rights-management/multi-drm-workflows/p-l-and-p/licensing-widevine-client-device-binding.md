---
description: I vissa fall kanske du vill hindra slutanvändare från att spela upp innehåll på flera enheter när innehållet köpts eller hyrts. Om kunden använder Expressplay kan detta göras genom att använda Expressplay-API:erna för att binda användarens Expressplay-token till användarens dator.
seo-description: I vissa fall kanske du vill hindra slutanvändare från att spela upp innehåll på flera enheter när innehållet köpts eller hyrts. Om kunden använder Expressplay kan detta göras genom att använda Expressplay-API:erna för att binda användarens Expressplay-token till användarens dator.
seo-title: Enhetsbindning
title: Enhetsbindning
uuid: 351fa33c-4226-4ed5-829c-56b563166fec
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Enhetsbindning{#device-binding}

I vissa fall kanske du vill hindra slutanvändare från att spela upp innehåll på flera enheter när innehållet köpts eller hyrts. Om kunden använder Expressplay kan detta göras genom att använda Expressplay-API:erna för att binda användarens Expressplay-token till användarens dator.

Du kan använda API:erna på följande sätt.

1. Generera en cookie.
1. Skicka en begäran om att skapa en overksam token med den genererade cookien kopplad som antingen en frågesträng (cookie=`<cookie>`) eller som rubriker.
1. Låt användarens dator skicka en licensbegäran till Expresshow-licensservern med hjälp av ovanstående token, till exempel genom att spela upp ett dummy-innehåll.

   När den här dummy-licensbegäran lyckas associerar den användarens device_id (beräknad eller genererad av DRM-implementeringen på användarens enhet) med cookien i Expressplay back-end. Denna cookie används sedan på följande sätt:

   * Vid köp/hyra av innehåll skickar koden en fråga till uttryckets back-end för användarens device_id genom att skicka den associerade cookien ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Skicka en begäran om tokengenerering med det köpta innehållets nyckel (CEK), keyID (CEKSID), principer och annan information och bifoga cookien och device_id ovan som `cookie`-korrelationsparametern respektive `deviceid`-tokenbegränsningsparametern.

   * Ange denna token för användaren.

      Den här processen genererar en token för innehållet som är bundet till användarens device_id. När användarens dator skickar en licensbegäran med denna token, kommer Expressplay back-end att kontrollera token&#39;s device_id med licensbegärans device_id.

      En exempeltillståndsserver för uttryck implementerar det här arbetsflödet.
