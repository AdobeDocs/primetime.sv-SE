---
seo-title: Identitetsbaserade domäner
title: Identitetsbaserade domäner
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Identitetsbaserade domäner {#identity-based-domains}

I det här fallet har varje autentiserad användare sin egen domän och ett visst antal enheter tillåts ansluta till domänen. Om du vill använda den här typen av domän med referensimplementeringen måste du skapa en profil som anger domänregistrering. Ange serverns värd och port för domänserverns URL och ange att autentisering av användarnamn/lösenord krävs.

Referensimplementeringen implementerar följande logik för domänregistrering:

1. Avgör vilket domännamn som ska tilldelas den här användaren. Domännamnet kommer att extraheras * `namequalifier:username`* från autentiseringstoken. Om det inte finns någon autentiseringstoken returnerar du felet DOM_AUTHENTICATION_REQUIRED (503).
1. Sök efter domännamnet i tabellen `DomainServerInfo`. Om ingen post hittas infogar du en post i tabellen (standardvärden är autentisering krävs, max domänmedlemskap=5).
1. Kontrollera om enheten redan har registrerats i domänen:

   1. Leta reda på domännamnet i tabellen `UserDomainMembership`. Jämför varje dator-ID som hittas med dator-ID i begäran. Om det här är en ny dator lägger du till en post i tabellen `UserDomainMembership`. Leta sedan reda på matchande poster i tabellen `UserDomainRefCount`. Lägg till en post om det inte finns någon post för det här maskin-GUID:t.

   1. Om det är en ny enhet och det maximala medlemskapet redan har nåtts returnerar du felet DOM_LIMIT_REACHED (502).

1. Sök efter alla domännycklar för den här domänen i tabellen DomainKeys.

   1. Om `DomainServerInfo` anger att nycklarna måste rullas över genererar du ett nytt nyckelpar, sparar det i tabellen `DomainKeys` (med nyckelversion ett högre än den högsta befintliga nyckeln) och återställer flaggan &quot;Key Rollover Required&quot; i `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

Referensimplementeringen implementerar följande logik för domänavregistrering:

1. Avgör vilket domännamn som ska tilldelas den här användaren. Domännamnet kommer att vara *namequalifier:användarnamn* som extraheras från autentiseringstoken. Om det inte finns någon autentiseringstoken returnerar du felet DOM_AUTHENTICATION_REQUIRED (503).
1. Sök efter det begärda domännamnet i tabellen `DomainServerInfo`.
1. Sök efter domännamnet i tabellen `UserDomainMembership`. Jämför varje dator-ID som hittas med dator-ID i begäran. Sök efter motsvarande post i tabellen `UserDomainRefCount`. Om ingen matchande post hittas returneras felet DEREG_DENIED (401).

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från tabellen `UserDomainRefCount`. Om det inte finns fler poster för datorn i tabellen tar du bort posten från `UserDomainMembership` och anger flaggan &quot;Key Rollover Required&quot; i `DomainServerInfo`.

I det här fallet får varje användare registrera ett litet antal datorer, så vi kan använda det fullständiga dator-ID:t och metoden `matches()` för att räkna antalet datorer korrekt. Eftersom användaren kan registrera flera gånger på den här datorn (via flera AIR-program eller spelare i olika webbläsare) måste servern också behålla ett referensantal, så att avregistreringen kan räknas korrekt. Avregistreringen kan inte anses vara slutförd förrän alla domäntoken på datorn har återgetts.
