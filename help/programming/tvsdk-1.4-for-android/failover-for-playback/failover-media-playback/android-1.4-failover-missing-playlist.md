---
description: När en hel spelningslista saknas, till exempel när M3U8-filen som anges i en manifestfil på översta nivån inte hämtas, försöker TVSDK att återställas. Om programmet inte kan återställas bestäms nästa steg.
seo-description: När en hel spelningslista saknas, till exempel när M3U8-filen som anges i en manifestfil på översta nivån inte hämtas, försöker TVSDK att återställas. Om programmet inte kan återställas bestäms nästa steg.
seo-title: Redundans för spelningslista saknas
title: Redundans för spelningslista saknas
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Redundans för spelningslista saknas{#missing-playlist-failover}

När en hel spelningslista saknas, till exempel när M3U8-filen som anges i en manifestfil på översta nivån inte hämtas, försöker TVSDK att återställas. Om programmet inte kan återställas bestäms nästa steg.

Om spelningslistan som är associerad med den mellanupplösta bithastigheten saknas söker TVSDK efter en variantspelningslista med samma upplösning. Om samma upplösning hittas börjar hämtningen av variantspellistan och segmenten från den matchande positionen. Om TVSDK inte hittar samma upplösningsspellista försöker den att bläddra igenom andra spellistor med bithastighet och deras varianter. En omedelbart lägre bithastighet är det första alternativet, dess variant och så vidare. Om alla spelningslistor med lägre bithastighet och deras varianter är utmattade i försöket att hitta en giltig spelningslista går TVSDK till den högsta bithastigheten och räknar ned därifrån. Om det inte går att hitta en giltig spelningslista misslyckas processen och spelaren övergår till FEL-läget.

Programmet kan avgöra hur den här situationen ska hanteras. Du kanske vill stänga spelaraktiviteten och dirigera användaren till katalogaktiviteten. Intressehändelsen är `STATE_CHANGED`-händelsen och motsvarande återanrop är `onStateChanged`-metoden. Här följer en kod som kontrollerar om spelaren ändrar sitt interna läge till FEL:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Mer information finns i [!DNL PlayerFragment.java]-filen i SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
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
