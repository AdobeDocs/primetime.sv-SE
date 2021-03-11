---
description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade medier.
title: Uppspelning och failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Uppspelning och failover {#playback-and-failover}

Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade medier.

Primetime kan inte skydda mot fel som ett avbrott i en Internet-leverantör eller en kabelbortkoppling. Primetime-strömning ger dock failover-skydd för att skydda uppspelningen från vissa fjärrserverfel eller driftfel, vilket ger en bättre upplevelse för tittarna. Webbläsare-TVSDK implementerar redundansskydd för att minimera uppspelningsavbrott och få en sömlös uppspelning trots överföringsproblem. Videospelaren växlar automatiskt till en uppsättning säkerhetskopieringsmedia när hela återgivningar eller fragment inte är tillgängliga.

## Medieuppspelning {#media-playback}

För live- och VOD-media startar Browser TVSDK uppspelningen genom att hämta den spellista som är associerad med den mellanupplösta bithastigheten och sedan hämta segment för den mellanupplösta bithastigheten som definieras av spellistan.

Browser TVSDK väljer snabbt den högupplösta spellistan med bithastighet och tillhörande media och fortsätter nedladdningen.

## Misslyckad spelningslista {#section_81A5822C108449E1A0E94A6E25DE9E8E}

När en hel spelningslista saknas, till exempel när M3U8-filen som anges i en manifestfil på den översta nivån inte hämtas, försöker webbläsaren TVSDK att återställas. Om det inte kan återställas bestäms nästa steg av programmet.

Om spelningslistan som är associerad med den mellanupplösta bithastigheten saknas söker webbläsaren TVSDK efter en variantspelningslista med samma upplösning. Om samma upplösning hittas börjar hämtningen av variantspellistan och segmenten från den matchande positionen. Om Browser TVSDK inte hittar samma upplösningsspellista försöker den bläddra igenom andra spellistor med bithastighet och deras varianter. En omedelbart lägre bithastighet är det första alternativet, dess variant och så vidare. Om alla spelningslistor med lägre bithastighet och deras varianter är utmattade i försöket att hitta en giltig spelningslista, kommer Browser TVSDK att gå till den övre bithastigheten och räkna ned därifrån. Om det inte går att hitta en giltig spelningslista misslyckas processen och spelaren övergår till FEL-läget.

Programmet kan avgöra hur den här situationen ska hanteras. Du kanske vill stänga spelaraktiviteten och dirigera användaren till katalogaktiviteten. Intressehändelsen är den statusändrade eller statusändrade händelsen och motsvarande återanrop är den metod som ändrats vid statusvärdet. Här följer en kod som kontrollerar om spelaren ändrar sitt interna läge till FEL:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
