---
title: Översikt
description: Översikt
copied-description: true
exl-id: 67c3d98f-8c17-4b5a-8abb-00f6f0f1e823
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Översikt {#overview}

*Paketering* avser processen att kryptera och tillämpa en profil på FLV- eller F4V-filer. Använd API:erna för mediepaketering för att paketera filer. Java SDK för Adobe Access kan bara paketera Flash och AIR-innehåll som FLV, F4V och MP4 för progressiv nedladdning. Om du vill paketera innehåll med Adobe Access DRM för andra innehållsformat, t.ex. Adobe HTTP Dynamic Streaming (HDS) eller Apple HTTP Live Streaming (HLS), måste du använda andra verktyg, t.ex. Adobe Media Server ( [https://www.adobe.com/products/adobe-media-server-family.html](https://www.adobe.com/products/adobe-media-server-family.html)) eller en kodare som implementerar SDK för Adobe-sändning ( [https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf](https://help.adobe.com/en_US/primetime/packagers/hdkb_api_overview_3.5.pdf)). Kunderna kan också välja att använda verktygsuppsättningen Adobe Java Primetime Packager, som kan paketera innehåll för en mängd olika målformat, till exempel HDS, HLS och DASH.

Paketeringen kopplas bort från licensservern. Paketeraren behöver inte ansluta till licensservern för att kunna utbyta information om innehållet. Allt licensservern behöver veta för att kunna utfärda licensen ingår i innehållets metadata.

När en fil är krypterad kan dess innehåll inte tolkas utan rätt licens. Med Adobe Access kan du välja vilka delar av filen som ska krypteras. Eftersom Adobe® Access™ kan tolka filformatet för FLV- och F4V-innehållet kan det kryptera selektiva delar av filen på ett intelligent sätt i stället för hela filen. Data som metadata och referenspunkter kan förbli okrypterade så att sökmotorer fortfarande kan söka i filen.

Ett visst innehåll kan ha flera principer. Detta kan vara användbart om du till exempel vill licensiera innehåll under olika affärsmodeller utan att behöva paketera innehållet flera gånger. Ni kan till exempel tillåta anonym åtkomst under en kort tidsperiod, och därefter kan kunden köpa innehållet och få obegränsad tillgång. Om innehållet paketeras med flera profiler måste licensservern implementera logik för att välja vilken policy som ska användas för att utfärda en licens.

>[!NOTE]
>
>Arkitekturen tillåter att användarprofiler anges och binds till innehåll när innehållet paketeras. Innan en klient kan spela upp innehåll måste klienten skaffa en licens för den datorn. Licensen anger de användningsregler som används och anger den nyckel som används för att dekryptera innehållet. Principen är en mall för att generera licensen, men licensservern kan välja att åsidosätta användningsreglerna när licensen utfärdas. Observera att licensen kan vara ogiltig genom begränsningar som förfallotider eller uppspelningsfönster.

Det finns många alternativ för att paketera innehåll. Dessa anges i `DRMParameters` -gränssnittet och klasserna som implementerar det gränssnittet, som är `F4VDRMParameters` och `FLVDRMParameters`. Med dessa klasser kan du ange signatur- och nyckelparametrar samt ange om ljudinnehåll, videoinnehåll eller skriptdata ska krypteras. Om du vill se hur dessa implementeras i referensimplementeringen läser du beskrivningarna av kommandoradsalternativen för Media Packager i *Använda referensimplementeringar för Adobe Access*. Dessa alternativ är baserade på Java API och är därför tillgängliga för programmatisk användning.

Paketeringsalternativen omfattar:

* Krypteringsalternativ (ljud, video, partiell kryptering).
* Licensserverns URL (klienten använder denna som bas-URL för alla begäranden som skickas till licensservern)
* Transportcertifikat för licensserver
* Licensservercertifikat som används för att kryptera CEK.
* Packager-autentiseringsuppgifter för signering av metadata

Adobe Access tillhandahåller ett API för att skicka CEK. Om inget CEK anges genereras det slumpmässigt av SDK. Vanligtvis behöver du olika CEK för varje del av innehållet. I Dynamic Streaming skulle du emellertid troligtvis använda samma CEK för alla filer för det innehållet, så användaren behöver bara en licens och kan smidigt gå över från en bithastighet till en annan. Om du vill använda samma nyckel och licens för flera innehållsdelar skickar du samma `DRMParameters` objekt till `MediaEncrypter.encryptContent()`eller skicka in CEK med `V2KeyParameters.setContentEncryptionKey()`. Om du vill använda olika nycklar och licenser för varje del av innehållet skapar du ett nytt `DRMParameters` -instans för varje fil.

När du paketerar innehåll med tangentrotation kan du styra vilka rotationstangenter som används och hur ofta tangenterna ändras. `F4VDRMParameters` och `FLVDRMParameters` implementera `KeyRotationParameters` gränssnitt. I det här gränssnittet kan du aktivera tangentrotation. Du måste också ange en `RotatingContentEncryptionKeyProvider`. För varje krypterat exempel avgör den här klassen vilken rotationsnyckel som ska användas. Du kan implementera din egen leverantör eller använda `TimeBasedKeyProvider` ingår i SDK. Implementeringen genererar slumpmässigt en ny nyckel efter ett angivet antal sekunder.

I vissa fall kan du behöva lagra innehållets metadata som en separat fil och göra den tillgänglig för klienten separat från innehållet. Det gör du genom att anropa `MediaEncrypter.encryptContent()`, som returnerar `MediaEncrypterResult` -objekt. Utlysning `MediaEncrypterResult.getKeyInfo()` och omvandla resultatet till `V2KeyStatus`. Hämta sedan innehållets metadata och lagra dem i en fil.

Alla dessa åtgärder kan utföras med Java API. Mer information om Java API som beskrivs i det här kapitlet finns i *API-referens för Adobe Access*.

Mer information om referensimplementeringen av Media Packager finns i *Använda referensimplementeringar för Adobe Access*.
