---
description: För live- och video-on-demand-media (VOD) börjar TVSDK uppspelningen genom att ladda ned den spellista som är associerad med den mellanupplösta bithastigheten och hämtar de mediesegment som definieras av spellistan. Den väljer snabbt spelningslistan med hög upplösning och tillhörande media och fortsätter hämtningsprocessen.
seo-description: För live- och video-on-demand-media (VOD) börjar TVSDK uppspelningen genom att ladda ned den spellista som är associerad med den mellanupplösta bithastigheten och hämtar de mediesegment som definieras av spellistan. Den väljer snabbt spelningslistan med hög upplösning och tillhörande media och fortsätter hämtningsprocessen.
seo-title: Medieuppspelning och failover
title: Medieuppspelning och failover
uuid: 197a6ee0-f1ff-40ac-bd49-eafeae6167d4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Medieuppspelning och failover{#media-playback-and-failover}

För live- och video-on-demand-media (VOD) börjar TVSDK uppspelningen genom att ladda ned den spellista som är associerad med den mellanupplösta bithastigheten och hämtar de mediesegment som definieras av spellistan. Den väljer snabbt spelningslistan med hög upplösning och tillhörande media och fortsätter hämtningsprocessen.

## Redundans för spelningslista saknas {#section_E6B6A15930894F56A0A8501577B35E7F}

När en hel spelningslista saknas, till exempel när M3U8-filen som anges i en manifestfil på översta nivån inte hämtas, försöker TVSDK att återställas. Om det inte kan återställas bestäms nästa steg av programmet.

Om spelningslistan som är associerad med den mellanupplösta bithastigheten saknas söker TVSDK efter en variantspelningslista med samma upplösning. Om samma upplösning hittas börjar hämtningen av variantspellistan och segmenten från den matchande positionen. Om TVSDK inte hittar samma upplösningsspellista försöker den att bläddra igenom andra spellistor med bithastighet och deras varianter. En omedelbart lägre bithastighet är det första alternativet, dess variant och så vidare. Om alla spelningslistor med lägre bithastighet och deras varianter är utmattade i försöket att hitta en giltig spelningslista går TVSDK till den högsta bithastigheten och räknar ned därifrån. Om det inte går att hitta en giltig spelningslista misslyckas processen och spelaren övergår till FEL-läget.

Programmet kan avgöra hur den här situationen ska hanteras. Du kanske vill stänga spelaraktiviteten och dirigera användaren till katalogaktiviteten. Intressehändelsen är `STATUS_CHANGED` händelsen och motsvarande återanrop är `onStatusChange` metoden. Här följer en kod som kontrollerar om spelaren ändrar sitt interna läge till FEL:

For more information, see the `PSDKDemo` file. Händelseavlyssnare är kopplade till MediaPlayer-instansen.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Om klientsidans nätverk inte fungerar kan du använda den här koden för att verifiera.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API kommer att tillhandahålla den URL som används för att verifiera om klientens nätverk är avstängt. Detta ska vara en giltig URL som returnerar http-svarskod 200 på http-begäranden.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Om setNetworkDownVerificationUrl inte är inställt använder TVSDK MainManifest-URL som standard för att ta reda på om nätverket är nere.

## segmentredundans saknas {#section_ED8CF666289042D39E9914D42BDD9BA4}

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
>ABR-styrparametrarna (Adaptive bit rate) beaktas inte när en växling vid fel inträffar. Detta beror på att failover-mekanismen är utformad för att använda någon av de spelningslistor som är tillgängliga, oavsett deras bithastighetsprofil, som säkerhetskopieringsströmmar.
>
>Under en redundansåtgärd kan det finnas en profilväxling. Om ett fel inträffar under hämtningen av ett av spellistsegmenten ignoreras ABR-kontrollparametrar som min/max tillåtna bithastighet.

