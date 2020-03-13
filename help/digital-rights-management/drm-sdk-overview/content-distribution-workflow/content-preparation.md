---
description: All användning av Adobe Primetime DRM består av två huvudsteg vid olika tidpunkter i arbetsflödet. Förberedelsen av innehållet måste göras en gång per resurs, vilket resulterar i att skyddat innehåll skapas. Inköp av innehåll görs flera gånger, en gång för varje konsument som vill titta på den skyddade resursen.
seo-description: All användning av Adobe Primetime DRM består av två huvudsteg vid olika tidpunkter i arbetsflödet. Förberedelsen av innehållet måste göras en gång per resurs, vilket resulterar i att skyddat innehåll skapas. Inköp av innehåll görs flera gånger, en gång för varje konsument som vill titta på den skyddade resursen.
seo-title: Förbereda innehåll
title: Förbereda innehåll
uuid: edb633f0-b623-41ea-a52a-19017d45fb18
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Förbereda innehåll{#content-preparation}

All användning av Adobe Primetime DRM består av två huvudsteg vid olika tidpunkter i arbetsflödet. Förberedelsen av innehållet måste göras en gång per resurs, vilket resulterar i att skyddat innehåll skapas. Inköp av innehåll görs flera gånger, en gång för varje konsument som vill titta på den skyddade resursen.

Innan du gör innehåll tillgängligt för distribution måste du först koda innehållet i videoformatet, skapa en eller flera profiler som anger användningsregler för innehållet och paketera innehållet med Adobe Primetime DRM SDK.

Stegen för att koda, paketera och distribuera innehåll är följande:

1. Koda innehållet i det videoformat du vill använda med kodningsverktyg från Adobe eller från tredje part.
1. Skapa profiler som anger de användningsregler som konsumenterna kan använda för att visa innehållet.

   En policy är behållaren för de regler och begränsningar som avgör hur, när och var det skyddade innehållet kan ses av konsumenterna.

   Paketeraren kräver minst en princip med minst en användningsregel. Du kan åsidosätta användningsregeln och lägga till ytterligare användningsregler när licensservern genererar licensen.

1. Paketera innehållet och ange vilka profiler som ska användas.

   Primetime DRM SDK krypterar innehållet med en innehållskrypteringsnyckel (CEK) och binder en eller flera profiler till innehållet. Resultatet är en *skyddad innehållsfil *som endast kan spelas upp av en konsument som har fått en licens från motsvarande licensserver.

   Under paketeringen krypteras innehållet med CEK. CEK krypteras med den offentliga nyckeln för licensservern och inkluderas i Primetimes DRM-metadata tillsammans med profilerna. DRM-metadata för Primetime signeras med den privata nyckeln för Packager och metadata inkluderas i det skyddade innehållet.

1. Gör det skyddade innehållet tillgängligt för distribution till konsumenter.

   Det skyddade innehållet distribueras vanligtvis via ett nätverk för innehållsdistribution (CDN). CDN kan använda vilken mekanism som helst som stöds av klientmiljön, som Flash Media Server, Adobe HTTP Dynamic Streaming för strömning med flera bithastigheter eller en HTTP Web Server för progressiv nedladdning.

