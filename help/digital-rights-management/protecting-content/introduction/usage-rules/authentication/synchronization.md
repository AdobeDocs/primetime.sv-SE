---
title: Krav för synkronisering
description: Krav för synkronisering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
