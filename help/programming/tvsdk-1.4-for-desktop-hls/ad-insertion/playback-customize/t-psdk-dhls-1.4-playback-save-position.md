---
description: Du kan spara den aktuella uppspelningspositionen i en video och återuppta uppspelningen på samma plats i en framtida session.
seo-description: Du kan spara den aktuella uppspelningspositionen i en video och återuppta uppspelningen på samma plats i en framtida session.
seo-title: Spara videopositionen och återuppta den senare
title: Spara videopositionen och återuppta den senare
uuid: 03ed5c63-008d-4dd1-9a31-baefa73b56e2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Spara videopositionen och återuppta den senare{#save-the-video-position-and-resume-later}

Du kan spara den aktuella uppspelningspositionen i en video och återuppta uppspelningen på samma plats i en framtida session.

Annonser som infogats dynamiskt skiljer sig mellan användarsessioner, så om du sparar positionen **med** delade annonser refererar till en annan position i en framtida session. TVSDK innehåller metoder för att hämta uppspelningspositionen samtidigt som delade annonser ignoreras.

1. När användaren avslutar en video hämtas och sparas positionen i videon.

   >[!TIP]
   >
   >Annonslängder ingår inte.

   Annonsbrytningar kan variera mellan olika sessioner på grund av annonsmönster, frekvensbegränsning och så vidare. Den aktuella tidpunkten för videon i en session kan vara annorlunda i en framtida session. När du sparar en position i videon hämtar programmet den lokala tiden. Använd egenskapen `localTime` för att läsa den här positionen, som du kan spara på enheten eller i en databas på servern.

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   Om användaren till exempel är på den 20:e minuten av videon, och den här positionen innehåller fem minuters annonser, kommer `currentTime` att `be` 1200 sekunder, medan `localTime` vid den här positionen kommer att vara `be` 900 sekunder.

1. Återställ användarsessionen när spelaraktiviteten återupptas.

   TVSDK återupptar inte uppspelningen mellan TVSDK-initieringar eftersom ingen information sparas lokalt. Programmet måste implementera den här logiken.

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. Så här återupptar du videon på samma plats:

   * Om du vill återuppta uppspelningen av videon från den position som sparades från en tidigare session använder du `seekToLocal`.

      >[!TIP]
      >
      >Den här metoden anropas bara med lokala tidsvärden. Om metoden anropas med aktuella tidsresultat inträffar ett felaktigt beteende.

   * Använd `seek` om du vill söka till aktuell tid.

1. När ditt program tar emot händelsen `onStatusChanged` för statusändring söker du efter den sparade lokala tiden.
1. Ange annonsbrytningarna som de anges i annonsprincipgränssnittet.
1. Implementera en anpassad annonsprincipväljare genom att utöka standardväljaren för annonsprinciper.
1. Ange de annonsbrytningar som måste presenteras för användaren genom att implementera `selectAdBreaksToPlay`.

   När spelaren anger statusen PREPARED är alla annonser redan lösta, så egenskapen `AdPolicyInfo.adBreakTimelineItem` innehåller alla annonsbrytningar före den lokala tidspositionen. Ditt program kan bestämma sig för att spela upp en annonsbrytning i förväg och återuppta den angivna lokala tiden, spela upp en annonsbrytning i mellanrummet och återuppta den angivna lokala tiden eller spela upp inga annonsbrytningar.
