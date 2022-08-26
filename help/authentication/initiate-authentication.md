---
title: Initiera autentisering
description: Initiera autentisering
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Initiera autentisering {#initiate-authentication}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## REST API-slutpunkter {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Beskrivning {#description}

Initierar autentiseringsprocessen genom att informera om en MVPD-markeringshändelse. Skapar en post i autentiseringsdatabasen Primetime, som synkroniseras när ett lyckat svar tas emot från PDF-filen. 



| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate | AuthN-modul | 1. request_id (obligatoriskt)</br>2.  mso_id (obligatoriskt)</br>3.  reg_kod (obligatoriskt)</br>4.  domain_name (obligatoriskt)</br>5.  noflash=true -  </br>    (Obligatoriskt, Resterande parameter)</br>6.  no_iframe=true (obligatorisk, rest-parameter)</br>7.  extra parametrar (valfritt)</br>8.  redirect_url (obligatoriskt) | GET | Inloggningswebbappen omdirigeras till inloggningssidan för MVPD. | 302 för fullständiga omdirigeringsimplementeringar |

{style=&quot;table-layout:auto&quot;}


| Indataparameter | Beskrivning |
| --- | --- |
| beställare_id | Den programmerarbegäran som den här åtgärden är giltig för. |
| mso_id | Det MVPD-ID som den här åtgärden gäller för. |
| reg_code | Registreringskoden som genereras av Reggie-tjänsten. |
| domain_name | Den ursprungliga domänen. |
| redirect_url | Omdirigerings-URL för inloggningswebbprogrammet efter att autentiseringen har slutförts. |

{style=&quot;table-layout:auto&quot;}

</br>

>[!IMPORTANT]
> 
>**Viktigt: Obligatoriska parametrar -** Oavsett implementering på klientsidan är alla parametrar ovan obligatoriska.
>
>
>Exempel:    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**Viktigt: Valfria parametrar**
>
>Anropet kan även innehålla valfria parametrar som möjliggör andra funktioner som:
>
> * generisk\_data - aktiverar användning av [TempPass för kampanjerbjudande](https://tve.helpdocsonline.com/promotional-temp-pass)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **Anteckningar** {#notes}

* Värdet för `domain_name` -parametern måste anges till ett av de domännamn som registrerats med Primetime-autentisering. Mer information finns i [Registrering och initiering](http://tve.helpdocsonline.com/new-programmer-overview$reg_and_init).

* [Undvik att använda &#39;&amp;&#39;reg\_code i /authenticate request (Tech Note)](https://tve.helpdocsonline.com/clientless:-avoid-using-&#39;&amp;&#39;reg_code-in-/authenticate-request)

* The `redirect_url` parametern måste vara den sista i ordningen

* Värdet för `redirect_url` parametern måste vara URL-kodad

[Tillbaka till REST API-referens](http://tve.helpdocsonline.com/rest-api-reference)
