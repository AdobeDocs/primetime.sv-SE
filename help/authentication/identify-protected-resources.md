---
title: Identifiera skyddade resurser
description: Identifiera skyddade resurser
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Identifiera skyddade resurser {#identifying-protected-resources}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Översikt {#overview}

Varje auktoriseringsbegäran (eller begäran om kontroll av auktorisering) måste innehålla en unik identifierare för den skyddade resurs som användaren begär åtkomst till. En skyddad resurs kan vara vilken nivå som helst av auktoriserat innehåll, enligt överenskommelse mellan en distributör och medverkande programmerare. Potentiella skyddade resurser måste passa in i denna trädstruktur av allt mer specifik granularitet:

- Nätverk
   - Kanal
      - Visa
         - Episod
            - Tillgång\
                

</br>

## Media RSS-format {#media_rss}

Resurser kan identifieras med en enkel sträng (en unik identifierare för en kanal) eller representeras i Media RSS-format (MRSS) enligt överenskommelse mellan Adobe (eller en auktoriserad partner för Adobe Primetime-autentisering) och deltagande programmerare och programmerare. Den RSS-sträng som används som resursspecificerare kan innehålla ytterligare information, till exempel klassificeringar och metadata för föräldrakontroll.\
 

Om du använder en enkel resursidentifierare, till exempel&quot;TNT&quot;, antas den representera en kanal och översätts till den här RSS-resursspecificeraren:

```RSS
    <rss version="2.0"> 
        <channel>
            <title>TNT</title>
        </channel>
    </rss>
```
 

En mer komplex specificerare kan t.ex. innehålla ytterligare klassificeringsinformation. Du kan skicka hela RSS-strängen till Access Enabler-funktioner som kräver ett resurs-ID, som [`getAuthorization()`](/help/authentication/rest-api-reference.md):

```rss
    var resource = 
        '<rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
             <channel>
                 <title>TNT</title>
                 <media:rating scheme="urn:mpaa">pg</media:rating>
             </channel>
         </rss>'; 
    getAuthorization(resource);
```

Resursspecifikationerna är ogenomskinliga för Adobe Primetime-autentisering. De skickas helt enkelt vidare till MVPD. Om MVPD inte känner igen eller kan tolka din resursspecificerare returneras ett fel till Adobe Primetime-autentiseringen, som skickar tillbaka felet till din `tokenRequestFailed()` återanrop.

<!--
## Related Information {#related}

-  User Metadata
-  Preflight Authorization
-->