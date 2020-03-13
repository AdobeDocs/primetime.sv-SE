---
description: 'null'
seo-description: 'null'
seo-title: Krav för synkronisering
title: Krav för synkronisering
uuid: 594a4bb2-c042-4485-9cae-73b8f9f93d82
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Krav för synkronisering {#requirements-for-synchronization}

Krav för synkronisering anger hur ofta klienten synkroniserar sitt tillstånd med servern. Om klienten har fått en out-of-band-licens (utan att någon licensserver kontaktas) kan användningsreglerna ange att klienten måste skicka synkroniseringsmeddelanden till servern för att synkronisera klientens säkra tid och rapportera klientens tillstånd till servern.

Synkroniseringsbeteendet definieras med följande parametrar:

* **Startintervall** - Anger hur lång tid det tar att vänta efter den senaste lyckade synkroniseringen för att starta en annan synkroniseringsbegäran.
* **Hårt stoppintervall** - (valfritt). Tillåt inte uppspelning om en lyckad synkronisering inte har utförts under den angivna tiden.
* **Tvinga synkroniseringssannolikhet** - (valfritt). Sannolikhet med vilken klienten ska skicka ett synkroniseringsmeddelande före nästa startintervall.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Den här användningsregeln stöds av Primetime DRM-klienter version 3.0 eller senare. Beteendet för äldre klienter beror på den lägsta klientversion som stöds av licensservern.

