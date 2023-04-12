---
title: Undvik att använda '&'reg_code i /authenticate Request
description: Undvik att använda '&'reg_code i /authenticate Request
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Undvik att använda &#39;&amp;&#39;reg_code i /authenticate Request {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>



## Problem

Webbläsaren IE 9 tolkar &#39;\®&#39; som ett specialkommando och konverterar det till ®. 

## Förklaring

Om `/authenticate` Begäran har följande sammansättning...

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...den tolkas av IE:s webbläsare som nedan och skickas till Adobe i detta format:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

Den som gjorde begäran\_id tolkas som univision®\_code=EKAFMFI, eftersom det inte finns något &#39;&amp;&#39; och Adobe kommer inte att hitta någon `regCode` param som token ska associeras med.  Det finns en risk att AuthN-token inte skapas alls, i så fall `/checkauthn` anrop kommer inte att hitta några tokens.



## Lösning

Ett av följande alternativ bör lösa problemet:

1. Undvik att använda `&reg_code` param mellan de andra frågesträngsparametrarna.  Flytta den i stället till den första frågesträngsparametern i begärande-URL:en så här:\
    

       &lt;fqdn>authenticate?reg_code =EKAFMFI&amp;requested_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   På det här sättet `&reg` param kommer inte att tolkas felaktigt.

1. Normalisera `&reg_code` som använder `&amp;reg_code`.

1. Adobe kan introducera en ny funktion för att skicka tillbaka en felkod till den andra skärmen som svar på ett autentiseringsanrop, om det inte gick att skapa AuthN-token.

