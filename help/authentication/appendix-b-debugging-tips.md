---
title: Bilaga B "Felsökningstips"
description: Bilaga B "Felsökningstips"
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Tillägg B: Felsökningstips {#appendix-b-debugging-tips}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Rensar temporära data {#clearing-temporary-data}

Adobe Primetime-autentisering lagrar tillfälliga data som webbläsarcache, LSO-cache och cookies. Det är viktigt att du rensar tillfälliga data för att vara säker på att du får en ren status när du testar.

- [Rensa webbläsarens cache och cookies](#clearing-the-browser-cache-and-cookies)
- [Rensar LSO-cache](#clearing-lsos-cache)\
    

## Rensa webbläsarens cache och cookies {#clearing-the-browser-cache-and-cookies}

Det är webbläsartillförlitligt, men i Firefox: &quot;Verktyg&quot; -\> &quot;Rensa senaste historik..&quot; -\> På &quot;Tidsintervall för att rensa:&quot; väljer du &quot;Allt&quot;; och på &quot;Detaljer&quot;: Markera&quot;Cookies&quot; och&quot;Cache&quot; -\> Klicka på&quot;Clear Now&quot;.\
 

## Rensar LSO-cache {#clearing-lsos-cache}

Öppna [Hjälp om Flash Player](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

Välj ```entitlement.\*``` (beroende på vad som har testats) och klicka på Ta bort webbplats.\
 

## Felsökningsverktyg {#tools}

Adobe Primetime autentiseringstekniker använder följande felsökningsverktyg:

- Firebug - <http://www.getfirebug.com/>
- Flashbug (fungerar med felsökningsversionen av Flash Player) <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Live http headers - <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Tråka - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->