---
title: Krav för synkronisering
description: Krav för synkronisering
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Krav för synkronisering{#requirements-for-synchronization}

Anger hur ofta klienten ska synkronisera sitt tillstånd med servern. Om klienten har fått en out-of-band-licens (utan att någon licensserver kontaktas) kan användningsreglerna ange att klienten måste skicka synkroniseringsmeddelanden till servern för att synkronisera klientens säkra tid och rapportera klientens tillstånd till servern.

Synkroniseringsbeteendet definieras med följande parametrar:

* Startintervall - Anger hur lång tid det tar att vänta efter den senaste lyckade synkroniseringen för att starta en annan synkroniseringsbegäran.
* Hårt stoppintervall - (valfritt). Tillåt inte uppspelning om en lyckad synkronisering inte har utförts under den angivna tiden.
* Tvinga synkroniseringssannolikhet - (valfritt). Sannolikhet med vilken klienten ska skicka ett synkroniseringsmeddelande före nästa startintervall.

>[!NOTE]
>
>Den här användningsregeln stöds av Adobe Access-klienter version 3.0 och senare. Beteendet för äldre klienter beror på den lägsta klientversion som stöds av licensservern. Se [Minsta klientversion](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

