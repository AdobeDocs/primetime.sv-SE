---
description: 'null'
seo-description: 'null'
seo-title: Anonym domänlogik
title: Anonym domänlogik
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Anonym domänlogik{#anonymous-domain-logic}

## Domänregistreringslogik {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

Referensimplementeringen använder följande logik för anonym domänregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Slå upp domännamnet i tabellen `DomainServerInfo`.
1. Om du inte hittar någon post infogar du en post i tabellen.

   Standardvärdena är:

   * `authentication is not required`
   * `no membership maximum`

   Om autentisering krävs för den begärda domänen kontrollerar du att det finns en giltig autentiseringstoken i begäran. Om autentiseringsnamnutrymmet anges i databasen måste token matcha det angivna autentiseringsnamnutrymmet.
1. Om autentisering krävs men ingen giltig autentiseringstoken är tillgänglig returnerar du felet `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Kontrollera om enheten är registrerad i domänen:

   1. Slå upp domännamnet i tabellen `DomainMembership`.
   1. Jämför det dator-GUID som du hittar med maskin-GUID i begäran.
   1. Om det här är en ny dator lägger du till en post i tabellen `DomainMembership`.
   1. Om det är en ny enhet och `Max Membership`-värdet har nåtts returnerar du felet `DOM_LIMIT_REACHED (502)`.

1. Slå upp alla domännycklar för den här domänen i tabellen `DomainKeys`:

   1. Generera ett nytt nyckelpar om `DomainServerInfo` anger att nycklarna måste rullas över.
   1. Spara nyckelparet i tabellen `DomainKeys` med en nyckelversion som är en siffra högre än den högsta befintliga nyckeln.
   1. Återställ flaggan `Key Rollover Required` i `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

## Avregistreringslogik för domän {#section_C968BBFCBFAB4510A903D169F38C9FCE}

Referensimplementeringen använder följande logik för anonym domänavregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Leta upp det begärda domännamnet i tabellen `DomainServerInfo`.
1. Om autentisering krävs för den begärda domänen kontrollerar du att det finns en giltig autentiseringstoken i begäran.

   Token måste också matcha det autentiseringsnamnutrymme som anges i databasen.
1. Slå upp domännamnet och datorns GUID i tabellen `DomainMembership`.

   Om du inte hittar någon matchande post returneras felet `DEREG_DENIED (401)`.

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `DomainMembership` och anger flaggan `Key Rollover Required` i `DomainServerInfo`.

Eftersom ett stort antal datorer kan ansluta till domänen kan du inte matcha dator-ID:t. I stället tillämpas det slumpmässiga maskin-GUID som tilldelas datorn under personaliseringen.
