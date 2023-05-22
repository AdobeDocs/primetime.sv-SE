---
title: Felsöka AccessEnabler iOS/tvOS SDK med hjälp av apploggarna i konsolen
description: Felsöka AccessEnabler iOS/tvOS SDK med hjälp av apploggarna i konsolen
exl-id: 0dad325e-db15-4ea0-a87a-75409eaf8d46
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Felsöka AccessEnabler iOS/tvOS SDK med hjälp av apploggarna i konsolen {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Översikt

Omfånget för det här dokumentet är att fånga och presentera utvecklingen av loggningsfunktionen i AccessEnablers iOS/tvOS SDK tillsammans med användbar information för felsökning av AccessEnabler-ramverket med hjälp av apploggarna i Console.

## Loggningsmekanismens tillstånd

Syftet med loggningsmekanismen i AccessEnabler iOS/tvOS är att generera användbara meddelanden för felsökning av eventuella problem som ett program som använder AccessEnabler-ramverket kan stöta på på grund av detta.

### AccessEnabler iOS/tvOS 3.5.0 och senare

Från och med AccessEnabler-versionen av iOS/tvOS 3.5.0 introducerar loggningsfunktionen följande förbättringar som ändringar:

* AccessEnabler-ramverket använder Apple som rekommenderas [OSLog](https://developer.apple.com/documentation/os/oslog) implementering.

* I AccessEnabler-ramverket introduceras möjligheten att filtrera konsolens apploggar baserat på undersystem: **com.adobe.pass.AccessEnabler**. Alla meddelanden som skickas av SDK är en del av com.adobe.pass.AccessEnabler.

* I AccessEnabler-ramverket introduceras möjligheten att filtrera konsolens apploggar baserat på Any (prefix): **[AccessEnabler]**. Alla meddelanden som skickas av SDK har prefix [AccessEnabler].

* I AccessEnabler-ramverket introduceras möjligheten att filtrera konsolens apploggar baserat på kategori: **debug**, **fel** tillsammans med något av de två ovanstående kriterierna: Delsystem eller Valfritt (prefix).

## Felsöka med hjälp av konsolapploggar

Beroende på vilka problem som utreds kanske du vill inkludera eller exkludera de loggningsmeddelanden som genereras av AccessEnabler-ramverket. Du kan därför nedan hitta användbar information som kan hjälpa dig vid utredningar och när du använder apploggar för Console.


### AccessEnabler iOS/tvOS 3.5.0 och senare

#### Inklusive {#including}

Först och främst för att kunna se alla loggningsmeddelanden som skickas av det AccessEnabler-ramverk du använder **måste** Markera&quot;Inkludera informationsmeddelanden&quot; och&quot;Inkludera felsökningsmeddelanden&quot; i delen Åtgärd i konsolappen enligt bilden nedan.

![](assets/include-info-debug-msg.png)


För att kunna felsöka funktionerna i AccessEnabler iOS/tvOS SDK och **se** I AccessEnabler-ramverket loggas du:

* Sök i konsolappen med **Delsystem** som är lika med värdet com.adobe.pass.AccessEnabler som i bilden nedan.

![](assets/subsys-console-app.png)

* Sök i konsolappen med **Alla** som innehåller
   [AccessEnabler] som i bilden nedan.

![](assets/any-optn-console-app.png)

Förutom ovanstående två villkor kan du också använda **Kategori** alternativ i konjugering med **Delsystem** eller **Valfritt (prefix)** att explicit söka efter **debug** eller **fel** nivåmeddelanden som skickas av AccessEnabler iOS/tvOS SDK.

#### Exklusive

För att bättre kunna felsöka funktionaliteten i andra komponenter och **exclude** I AccessEnabler-ramverket loggas du:

* Sök i konsolappen med **Delsystem** som inte är lika med värdet com.adobe.pass.AccessEnabler.
* Sök i konsolappen med **Alla** som inte innehåller [AccessEnabler] värde.

## Rapportera ett problem

När du rapporterar ett problem med Adobe Primetime-autentisering bör du överväga följande förslag:

* Var god försök att tillhandahålla reproduktionsstegen.
* Försök att ange den eller de operativsystemsversioner och enhetsmodeller som problemet gäller.
* Ange vilken version av AccessEnabler iOS/tvOS SDK som har problem.
* försök hämta och bifoga alla loggningsmeddelanden för AccessEnabler iOS/tvOS SDK med något av de två alternativen i [Inklusive](#including) -avsnitt.
