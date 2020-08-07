---
seo-title: Förbättrad kedja av licenser
title: Förbättrad kedja av licenser
uuid: 5e4e825a-de84-4ab2-a652-02cc03153957
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Förbättrad kedja av licenser {#enhanced-license-chaining}

Du kan använda den förbättrade licenskedjan för att uppdatera en licens genom att använda en överordnad rotlicens för batchuppdatering av licenser.

Primetime DRM 2.0 har stöd för licenssammanlänkning där både löv- och rotlicenserna är bundna till en viss dator. Primetime DRM 3.0 och senare har stöd för förbättrad licenskedning, där ett löv är bundet till en rotlicens och endast rotlicensen är bunden till en viss dator eller domän. Den förbättrade kedjan av licenser har stöd för att bädda in en lövlicens med innehållet, och klienten behöver bara skaffa rotlicensen från licensservern för att kunna använda det skyddade innehållet.

Om du vill aktivera förbättrad licenssammanlänkning måste du tilldela en rotkrypteringsnyckel till en Primetime DRM-princip. Rotkrypteringsnyckeln används för att kryptografiskt binda bladlicensen till rotlicensen.

>[!NOTE]
>
>Förbättrad kedja av licenser stöds av Primetime DRM-klienter version 3.0 eller senare. Om en äldre klient begär en licens för innehåll som har stöd för den förbättrade licenskedjan kan licensservern fortfarande utfärda en licens till den här klienten genom att använda den licenssammankoppling som stöds av Primetime DRM 2.0.

Exempel: Använd det här alternativet om du vill uppdatera länkade licenser genom att hämta en enda rotlicens. Implementera t.ex. prenumerationsmodeller där innehållet kan spelas upp så länge som användaren förnyar prenumerationen på månadsbasis. Fördelen med detta är att användarna bara behöver skaffa en enda licens för att uppdatera alla sina prenumerationslicenser.
