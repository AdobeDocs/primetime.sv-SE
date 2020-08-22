---
description: För live- och video-on-demand-media (VOD) börjar TVSDK uppspelningen genom att ladda ned den spellista som är associerad med den mellanupplösta bithastigheten och hämtar de mediesegment som definieras av den spellistan. Den väljer snabbt spelningslistan med hög upplösning och tillhörande media och fortsätter hämtningsprocessen.
seo-description: För live- och video-on-demand-media (VOD) börjar TVSDK uppspelningen genom att ladda ned den spellista som är associerad med den mellanupplösta bithastigheten och hämtar de mediesegment som definieras av den spellistan. Den väljer snabbt spelningslistan med hög upplösning och tillhörande media och fortsätter hämtningsprocessen.
seo-title: Medieuppspelning och failover
title: Medieuppspelning och failover
uuid: e0072eeb-8ad1-436f-bf4a-fee6885a25bd
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---


# Medieuppspelning och failover {#media-playback-and-failover}

För live- och video-on-demand-media (VOD) börjar TVSDK uppspelningen genom att ladda ned den spellista som är associerad med den mellanupplösta bithastigheten och hämtar de mediesegment som definieras av den spellistan. Den väljer snabbt spelningslistan med hög upplösning och tillhörande media och fortsätter hämtningsprocessen.

## Redundans för spelningslista saknas {#section_4EA0AEFA7FB84FCEA699DFB10B135368}

När en hel spelningslista saknas, till exempel om M3U8-filen som anges i en manifestfil på den översta nivån inte hämtas, försöker TVSDK att återställas. Om det inte kan återställas bestäms nästa steg av programmet.

Om spelningslistan som är associerad med den mellanupplösta bithastigheten saknas söker TVSDK efter en variantspelningslista med samma upplösning. Om samma upplösning hittas börjar TVSDK att hämta variantspellistan och segmenten från den matchande positionen. Om spelaren inte hittar samma upplösningsspellista kommer den att försöka bläddra igenom andra spellistor med bithastighet och deras varianter. En omedelbart lägre bithastighet är det första alternativet, dess variant och så vidare. Om alla spelningslistor med lägre bithastighet och deras varianter är utmattade i försöket att hitta en giltig spelningslista går TVSDK till den högsta bithastigheten och räknar ned därifrån. Om det inte går att hitta en giltig spelningslista misslyckas processen och spelaren övergår till FEL-läget.

Programmet kan avgöra hur den här situationen ska hanteras. Du kanske vill stänga spelaraktiviteten och dirigera användaren till katalogaktiviteten. Intressehändelsen är `STATUS_CHANGED` händelsen och motsvarande återanrop är `onStatusChanged` metoden. Här är koden som övervakar om spelaren ändrar sin interna status till `ERROR`:

```java
... 
case ERROR: 
getActivity().finish(); // this is where we close the current activity (the Player activity) 
break; 
...
```

## segmentredundans saknas {#section_D8DF377CCB644D7FB936796DA0CC5A4B}

När ett segment saknas, till exempel om ett visst segment inte kan hämtas, försöker TVSDK att återställas genom en mängd olika redundansförsök. Om det inte går att återställa genereras ett fel.

Om ett segment saknas på servern, till exempel på grund av att manifestfilen inte finns, kan segmentet inte laddas ned och så vidare, försöker TVSDK att redundansväxla genom att försöka med följande alternativ:

1. Försök med en växling vid fel till samma segment, med samma bithastighet, i en variantfil.
1. Växla till en alternativ bithastighet (ABR-switch) i samma fil.
1. Bläddra igenom alla tillgängliga bithastigheter i alla tillgängliga varianter.
1. Hoppa över segmentet och skicka en varning.

När TVSDK inte kan hämta ett alternativt segment utlöses ett `CONTENT_ERROR` felmeddelande. Det här meddelandet innehåller ett internt meddelande med `DOWNLOAD_ERROR` koden. Om strömmen med problemet är ett alternativt ljudspår genererar TVSDK felmeddelandet `AUDIO_TRACK_ERROR` .

Om videomotorn inte kontinuerligt kan hämta segment begränsas antalet kontinuerliga segmenthopp till 5, varefter uppspelningen stoppas och TVSDK utfärdar en kod `NATIVE_ERROR` med koden 5.

>[!NOTE]
>
>**Begränsningar**
>
>Här är några begränsningar som du bör känna till:
>
>* ABR-styrparametrarna (Adaptive bit rate) beaktas inte när en växling vid fel inträffar.
>
>  
Detta beror på att failover-mekanismen är utformad för att använda någon av de spelningslistor som är tillgängliga, oavsett bithastighetsprofil, som säkerhetskopieringsströmmar.
>* Under en redundansåtgärd kan det finnas en profilväxling.
>
>  
Om ett fel inträffar under hämtningen av ett av spellistsegmenten ignoreras ABR-kontrollparametrar som min/max tillåtna bithastighet.
