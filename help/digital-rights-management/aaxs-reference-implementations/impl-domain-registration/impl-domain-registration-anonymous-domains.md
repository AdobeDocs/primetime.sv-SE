---
title: Anonyma domäner
description: Anonyma domäner
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Anonyma domäner {#anonymous-domains}

I det här fallet tillhör ett stort antal enheter en enda domän och autentisering kanske inte krävs. Om du vill använda den här typen av domän med referensimplementeringen skapar du principen som anger att domänregistrering krävs. Ange domänserverns URL som `https:// host:port/flashaccess/domainserver/domainname/` och ange anonym autentisering.

Referensimplementeringen implementerar följande logik för domänregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Sök efter domännamnet i dialogrutan `DomainServerInfo` tabell. Om en post inte hittas infogar du en post i tabellen (standardvärden: autentisering krävs inte och inget maximalt medlemskap krävs).
1. Om autentisering krävs för den begärda domänen kontrollerar du att en giltig autentiseringstoken har inkluderats i begäran och att den matchar autentiseringsnamnutrymmet, om det har angetts i databasen.

   1. Om autentisering krävs men ingen giltig auth-token har angetts returneras fel `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Kontrollera om enheten redan har registrerats i domänen:

   1. Sök efter domännamnet i dialogrutan `DomainMembership` tabell. Jämför varje dator-GUID som hittas med maskin-GUID i begäran. Om det här är en ny dator lägger du till en post i `DomainMembership` tabell.

   1. Om det är en ny enhet och det maximala medlemskapet redan har nåtts returneras ett fel `DOM_LIMIT_REACHED (502)`.

1. Sök efter alla domännycklar för den här domänen i `DomainKeys` tabell.

   1. If `DomainServerInfo` anger att tangenterna måste rullas över, skapar ett nytt nyckelpar och sparar det i `DomainKeys` tabell (med nyckelversion ett högre än den högsta befintliga tangenten) och återställa `Key Rollover Required` flagga in `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

Referensimplementeringen implementerar följande logik för domänavregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Sök efter det begärda domännamnet i `DomainServerInfo` tabell.
1. Om autentisering krävs för den begärda domänen kontrollerar du att en giltig autentiseringstoken har inkluderats i begäran och att den matchar autentiseringsnamnutrymmet, om det har angetts i databasen.
1. Sök efter domännamnet och datorns GUID i `DomainMembership` tabell. Om ingen matchande post hittas returneras felet `DEREG_DENIED (401)`.

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `DomainMembership` och ange `Key Rollover Required` flagga in `DomainServerInfo`.

I det här fallet är det inte möjligt att matcha dator-ID:t fullständigt eftersom ett stort antal datorer kan ansluta till domänen. I stället används det slumpmässiga maskin-GUID som tilldelats datorn under personaliseringen.
