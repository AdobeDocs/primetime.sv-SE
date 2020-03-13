---
description: TVSDK kontaktar en annonsleveranstjänst, till exempel Adobe Primetimes annonsbeslut, och försöker hämta den primära spellistfilen som motsvarar annonsens videoström. Under reklamlösningsfasen gör TVSDK ett HTTP-anrop till den fjärranslutna annonsservern och tolkar serverns svar.
seo-description: TVSDK kontaktar en annonsleveranstjänst, till exempel Adobe Primetimes annonsbeslut, och försöker hämta den primära spellistfilen som motsvarar annonsens videoström. Under reklamlösningsfasen gör TVSDK ett HTTP-anrop till den fjärranslutna annonsservern och tolkar serverns svar.
seo-title: Ad-resolving phase
title: Ad-resolving phase
uuid: b3e62a57-7e62-4e4e-8fa6-0d416785db67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ad-resolving phase{#ad-resolving-phase}

TVSDK kontaktar en annonsleveranstjänst, till exempel Adobe Primetimes annonsbeslut, och försöker hämta den primära spellistfilen som motsvarar annonsens videoström. Under reklamlösningsfasen gör TVSDK ett HTTP-anrop till den fjärranslutna annonsservern och tolkar serverns svar.

TVSDK har stöd för följande typer av annonsleverantörer:

* Metadata och leverantör

   Annonsdata kodas i JSON-filer med oformaterad text.
* Annonsleverantör för Primetime-annonsbeslut

   TVSDK skickar en begäran, inklusive en uppsättning parametrar för målinriktning och ett resursidentifieringsnummer, till den bakomliggande servern för Primetime-annonsbeslut. Primetime-annonsbeslut svarar med ett SMIL-dokument (synkroniserat multimedieintegrationsspråk) som innehåller den annonseringsinformation som krävs.
* Anordnare av anpassade annonser

   Hanterar situationen där annonser bränns in i strömmen från serversidan. TVSDK utför inte den faktiska annonsinfogningen, men det måste hålla reda på de annonser som infogades på serversidan. Den här providern ställer in annonsmarkörerna som TVSDK använder för att utföra annonsspårningen.

En av följande redundanssituationer kan uppstå under den här fasen:

* Det går inte att hämta data på grund av bl.a. bristande anslutning eller fel på serversidan, t.ex. att en resurs inte kan hittas osv.
* Data hämtades, men formatet är ogiltigt.

   Detta kan inträffa till exempel på grund av att tolkningen av inkommande data misslyckades.

TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.
