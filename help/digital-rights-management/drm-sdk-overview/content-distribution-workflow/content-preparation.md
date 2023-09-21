---
description: All användning av Adobe Primetime DRM består av två huvudsteg vid olika tidpunkter i arbetsflödet. Förberedelsen av innehållet måste göras en gång per resurs, vilket resulterar i att skyddat innehåll skapas. Inköp av innehåll görs flera gånger, en gång för varje konsument som vill titta på den skyddade resursen.
title: Förbereda innehåll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Förbereda innehåll{#content-preparation}

All användning av Adobe Primetime DRM består av två huvudsteg vid olika tidpunkter i arbetsflödet. Förberedelsen av innehållet måste göras en gång per resurs, vilket resulterar i att skyddat innehåll skapas. Inköp av innehåll görs flera gånger, en gång för varje konsument som vill titta på den skyddade resursen.

Innan du gör innehåll tillgängligt för distribution måste du först koda innehållet i videoformatet, skapa en eller flera profiler som anger användningsregler för innehållet och paketera innehållet med Adobe Primetime DRM SDK.

Stegen för att koda, paketera och distribuera innehåll är följande:

1. Koda materialet i det videoformat du önskar med kodningsverktygen från Adobe eller från tredje part.
1. Skapa profiler som specificerar de användningsregler som konsumenterna kan använda för att visa innehållet.

   En policy är behållaren för de regler och begränsningar som avgör hur, när och var det skyddade innehållet kan ses av konsumenterna.

   Packager kräver minst en princip med minst en användningsregel. Du kan åsidosätta användningsregeln och lägga till ytterligare användningsregler när licensservern genererar licensen.

1. Paketera innehållet och ange vilka profiler som ska användas.

   Primetime DRM SDK krypterar innehållet med en innehållskrypteringsnyckel (CEK) och binder en eller flera profiler till innehållet. Resultatet är en *skyddad innehållsfil *som endast kan spelas upp av en konsument som har fått en licens från motsvarande licensserver.

   Under paketeringen krypteras innehållet med CEK. CEK krypteras med den offentliga nyckeln för licensservern och inkluderas i Primetimes DRM-metadata tillsammans med profilerna. DRM-metadata för Primetime signeras med den privata nyckeln för Packager och metadata inkluderas i det skyddade innehållet.

1. Gör det skyddade innehållet tillgängligt för distribution till konsumenter.

   Det skyddade innehållet distribueras vanligtvis via ett nätverk för innehållsdistribution (CDN). CDN kan använda vilken mekanism som helst som stöds av klientmiljön, till exempel Flash Media Server, Adobe HTTP Dynamic Streaming för direktuppspelning med flera bithastigheter eller en HTTP-webbserver för progressiv nedladdning.
