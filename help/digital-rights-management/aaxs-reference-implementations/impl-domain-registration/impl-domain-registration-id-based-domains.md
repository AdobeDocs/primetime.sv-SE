---
title: Identitetsbaserade domäner
description: Identitetsbaserade domäner
copied-description: true
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Identitetsbaserade domäner {#identity-based-domains}

I det här fallet har varje autentiserad användare sin egen domän och ett visst antal enheter tillåts ansluta till domänen. Om du vill använda den här typen av domän med referensimplementeringen måste du skapa en profil som anger domänregistrering. Ange serverns värd och port för domänserverns URL och ange att autentisering av användarnamn/lösenord krävs.

Referensimplementeringen implementerar följande logik för domänregistrering:

1. Avgör vilket domännamn som ska tilldelas den här användaren. Domännamnet är * `namequalifier:username`* extraherat från autentiseringstoken. Om det inte finns någon autentiseringstoken returnerar du felet DOM_AUTHENTICATION_REQUIRED (503).
1. Sök efter domännamnet i `DomainServerInfo` tabell. Om ingen post hittas infogar du en post i tabellen (standardvärden är autentisering krävs, max domänmedlemskap=5).
1. Kontrollera om enheten redan har registrerats i domänen:

   1. Sök efter domännamnet i dialogrutan `UserDomainMembership` tabell. Jämför varje dator-ID som hittas med dator-ID i begäran. Om det här är en ny dator lägger du till en post i `UserDomainMembership` tabell. Leta reda på matchande poster i `UserDomainRefCount` tabell. Lägg till en post om det inte finns någon post för det här maskin-GUID:t.

   1. Om det är en ny enhet och det maximala medlemskapet redan har nåtts returnerar du felet DOM_LIMIT_REACHED (502).

1. Sök efter alla domännycklar för den här domänen i tabellen DomainKeys.

   1. If `DomainServerInfo` anger att nycklarna måste rullas över, generera ett nytt nyckelpar och spara det i `DomainKeys` tabell (med nyckelversion ett högre än den högsta befintliga nyckeln) och återställ flaggan&quot;Key Rollover Required&quot; i `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

Referensimplementeringen implementerar följande logik för domänavregistrering:

1. Avgör vilket domännamn som ska tilldelas den här användaren. Domännamnet blir *namequalifier:användarnamn* extraheras från autentiseringstoken. Om det inte finns någon autentiseringstoken returnerar du felet DOM_AUTHENTICATION_REQUIRED (503).
1. Sök efter det begärda domännamnet i `DomainServerInfo` tabell.
1. Sök efter domännamnet i `UserDomainMembership` tabell. Jämför varje dator-ID som hittas med dator-ID i begäran. Sök efter motsvarande post i `UserDomainRefCount` tabell. Om ingen matchande post hittas returneras felet DEREG_DENIED (401).

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `UserDomainRefCount` tabell. Om det inte finns fler poster i tabellen för datorn tar du bort posten från `UserDomainMembership` och ange flaggan&quot;Key Rollover Required&quot; i `DomainServerInfo`.

I det här fallet får varje användare registrera ett litet antal datorer, så vi kan använda hela dator-ID:t och `matches()` metod för korrekt räkning av datorer. Eftersom användaren kan registrera flera gånger på den här datorn (via flera AIR-program eller spelare i olika webbläsare) måste servern också behålla ett referensantal, så att avregistreringen kan räknas korrekt. Avregistreringen kan inte anses vara slutförd förrän alla domäntoken på datorn har återgetts.
