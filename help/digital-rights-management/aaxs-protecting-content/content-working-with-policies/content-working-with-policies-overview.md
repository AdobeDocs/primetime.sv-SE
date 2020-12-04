---
seo-title: Översikt
title: Översikt
uuid: 7363d241-6947-4a9c-80e5-e50be71066b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Översikt {#overview}

Med Adobe® Access™ kan innehållsleverantörer tillämpa regler på mediefiler. Med hjälp av API:erna för principhantering kan administratörer skapa, visa information om och uppdatera principer.

En *policy* definierar hur användare kan visa innehåll; det är en samling information som innehåller säkerhetsinställningar, autentiseringskrav och användarrättigheter. När regler tillämpas tillåter kryptering och signering att innehållsleverantörer behåller kontrollen över sitt innehåll oavsett hur brett det distribueras. Skyddade filer kan levereras med Adobe® Flash® Media Server eller en HTTP-server. De kan laddas ned och spelas upp i anpassade spelare som skapats med Adobe® AIR®, Adobe® Flash® Player och Adobe® Primetime SDK för iOS. Principen är en mall som licensservern kan använda när den genererar en licens. Klienten kan också hänvisa till policyn innan han begär en licens för att avgöra om han eller hon måste be användaren autentisera innan han eller hon skickar en licensbegäran till servern.

En princip anger en eller flera rättigheter som beviljas klienten. En profil innehåller vanligtvis minst&quot;Spela upp höger&quot;. Det går också att ange flera uppspelningsrättigheter, var och en med olika begränsningar. När klienten påträffar en licens med flera uppspelningsrättigheter, används den första som den uppfyller alla begränsningar för. Den här funktionen kan till exempel användas för att tillämpa olika inställningar för utdataskydd på olika plattformar. Exempelkod som illustrerar det här exemplet finns i `CreatePolicyWithOutputProtection.java` i katalogen &quot;samples&quot; i Command Line Tools för Reference Implementation.

Du kan utföra följande åtgärder med hjälp av API:erna för principhantering:

* Skapa och uppdatera policyer
* Visa policyinformation
* Hantera listor för principuppdatering

Mer information om Java API som diskuteras i det här kapitlet finns i *API-referens för Adobe Access*.

Mer information om referensimplementeringen av principhanteraren finns i *Använda referensimplementeringar för Adobe Access*.
