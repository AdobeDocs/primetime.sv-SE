---
title: Krav för synkronisering
description: Krav för synkronisering
copied-description: true
exl-id: 0368e363-893f-4b51-a317-00791d0ab54f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Krav för synkronisering {#requirements-for-synchronization}

Krav för synkronisering anger hur ofta klienten synkroniserar sitt tillstånd med servern. Om klienten har fått en out-of-band-licens (utan att någon licensserver kontaktas) kan användningsreglerna ange att klienten måste skicka synkroniseringsmeddelanden till servern för att synkronisera klientens säkra tid och rapportera klientens tillstånd till servern.

Synkroniseringsbeteendet definieras med följande parametrar:

* **Startintervall** - Anger hur lång tid det tar att vänta efter den senaste lyckade synkroniseringen för att starta en annan synkroniseringsbegäran.
* **Hårt stoppintervall** - (Valfritt). Tillåt inte uppspelning om en lyckad synkronisering inte har utförts under den angivna tiden.
* **Tvinga synkroniseringssannolikhet** - (Valfritt). Sannolikhet med vilken klienten ska skicka ett synkroniseringsmeddelande före nästa startintervall.

>[!NOTE]
>
>Den här användningsregeln stöds av Primetime DRM-klienter version 3.0 eller senare. Beteendet för äldre klienter beror på den lägsta klientversion som stöds av licensservern.
