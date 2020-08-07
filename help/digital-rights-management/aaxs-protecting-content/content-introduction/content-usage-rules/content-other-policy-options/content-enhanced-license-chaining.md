---
seo-title: Förbättrad kedja av licenser
title: Förbättrad kedja av licenser
uuid: d11b0631-5dfb-42b8-b7ba-cfeb1da488be
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Förbättrad kedja av licenser {#enhanced-license-chaining}

Tillåter att en licens uppdateras med en överordnad rotlicens för batchuppdatering av licenser.

Adobe Access 2.0-stödd kedja av licenser där både löv- och rotlicenserna är bundna till en viss dator. Adobe Access 3.0 har stöd för förbättrad licenssammanlänkning, där ett löv är bundet till en rotlicens och endast rotlicensen är bunden till en viss dator eller domän. Den förbättrade kedjan av licenser stöder inbäddning av bladlicenser med innehållet, och klienten behöver bara skaffa rotlicensen från licensservern för att kunna använda det skyddade innehållet.

Om du vill aktivera den utökade licenskedjan tilldelas en rotkrypteringsnyckel till profilen. Rotkrypteringsnyckeln används för att kryptografiskt binda bladlicensen till rotlicensen.

>[!NOTE]
>
>Den förbättrade kedjan av licenser stöds av Adobe Access-klienter version 3.0 och senare. Om en äldre klient begär en licens för innehåll som har stöd för den förbättrade licenskedjan kan licensservern fortfarande utfärda en licens till den här klienten med hjälp av licenskedjan som stöds av Adobe Access 2.0.

Exempel: Använd det här alternativet om du vill uppdatera länkade licenser genom att hämta en enda rotlicens. Implementera t.ex. prenumerationsmodeller där innehållet kan spelas upp så länge som användaren förnyar prenumerationen på månadsbasis. Fördelen med detta är att användarna bara behöver göra ett enda licensförvärv för att uppdatera alla sina prenumerationslicenser.
