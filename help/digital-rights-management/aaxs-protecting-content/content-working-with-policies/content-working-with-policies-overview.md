---
title: Ökning
description: Ökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Ökning  {#overview}

Med Adobe® Access™ kan innehållsleverantörer tillämpa regler på mediefiler. Med hjälp av API:erna för principhantering kan administratörer skapa, visa information om och uppdatera principer.

A *policy* definierar hur användare kan visa innehåll. Det är en samling information som innehåller säkerhetsinställningar, autentiseringskrav och användarrättigheter. När regler tillämpas tillåter kryptering och signering innehållsleverantörer att behålla kontrollen över sitt innehåll oavsett hur brett det distribueras. Skyddade filer kan levereras med Adobe® Flash® Media Server eller en HTTP-server. De kan laddas ned och spelas upp i anpassade spelare som skapats med Adobe® AIR®, Adobe® Flash® Player och Adobe® Primetime SDK för iOS. Principen är en mall som licensservern kan använda när den genererar en licens. Klienten kan också hänvisa till policyn innan han begär en licens för att avgöra om han eller hon måste be användaren autentisera innan han eller hon skickar en licensbegäran till servern.

En princip anger en eller flera rättigheter som beviljas klienten. En profil innehåller vanligtvis minst&quot;Spela upp höger&quot;. Det går också att ange flera uppspelningsrättigheter, var och en med olika begränsningar. När klienten påträffar en licens med flera uppspelningsrättigheter, används den första som den uppfyller alla begränsningar för. Den här funktionen kan till exempel användas för att tillämpa olika inställningar för utdataskydd på olika plattformar. Exempelkod som illustrerar det här exemplet finns i `CreatePolicyWithOutputProtection.java` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.

Du kan utföra följande åtgärder med hjälp av API:erna för principhantering:

* Skapa och uppdatera policyer
* Visa policyinformation
* Hantera listor för principuppdatering

Mer information om Java API som beskrivs i det här kapitlet finns i *API-referens för Adobe Access*.

Mer information om implementeringen av principhanterarens referens finns i *Använda referensimplementeringar för Adobe Access*.
