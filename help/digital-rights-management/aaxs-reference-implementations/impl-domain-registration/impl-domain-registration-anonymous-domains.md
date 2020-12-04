---
seo-title: Anonyma domäner
title: Anonyma domäner
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Anonyma domäner {#anonymous-domains}

I det här fallet tillhör ett stort antal enheter en enda domän och autentisering kanske inte krävs. Om du vill använda den här typen av domän med referensimplementeringen skapar du principen som anger att domänregistrering krävs. Ange domänserverns URL som `https:// host:port/flashaccess/domainserver/domainname/` och ange anonym autentisering.

Referensimplementeringen implementerar följande logik för domänregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Sök efter domännamnet i tabellen `DomainServerInfo`. Om ingen post hittas infogar du en post i tabellen (standardvärden: autentisering krävs inte och inget medlemskap är maximalt).
1. Om autentisering krävs för den begärda domänen kontrollerar du att en giltig autentiseringstoken har inkluderats i begäran och att den matchar autentiseringsnamnutrymmet, om det har angetts i databasen.

   1. Om autentisering krävs men ingen giltig auth-token har angetts returnerar du felet `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Kontrollera om enheten redan har registrerats i domänen:

   1. Sök efter domännamnet i tabellen `DomainMembership`. Jämför varje dator-GUID som hittas med maskin-GUID i begäran. Om det här är en ny dator lägger du till en post i tabellen `DomainMembership`.

   1. Om det är en ny enhet och det maximala medlemskapet redan har nåtts returnerar du felet `DOM_LIMIT_REACHED (502)`.

1. Sök efter alla domännycklar för den här domänen i tabellen `DomainKeys`.

   1. Om `DomainServerInfo` anger att nycklarna måste rullas över genererar du ett nytt nyckelpar, sparar det i tabellen `DomainKeys` (med nyckelversion ett högre än den högsta befintliga nyckeln) och återställer flaggan `Key Rollover Required` i `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

Referensimplementeringen implementerar följande logik för domänavregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Sök efter det begärda domännamnet i tabellen `DomainServerInfo`.
1. Om autentisering krävs för den begärda domänen kontrollerar du att en giltig autentiseringstoken har inkluderats i begäran och att den matchar autentiseringsnamnutrymmet, om det har angetts i databasen.
1. Sök efter domännamnet och datorns GUID i tabellen `DomainMembership`. Om ingen matchande post hittas returneras felet `DEREG_DENIED (401)`.

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `DomainMembership` och anger flaggan `Key Rollover Required` i `DomainServerInfo`.

I det här fallet går det inte att matcha dator-ID:t fullständigt eftersom ett stort antal datorer kan ansluta till domänen. I stället används det slumpmässiga maskin-GUID som tilldelats datorn under personaliseringen.
