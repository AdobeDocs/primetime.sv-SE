---
title: Anonym domänlogik
description: Anonym domänlogik
copied-description: true
exl-id: 4a6c3485-cde7-403f-89d8-f6420df3539a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Anonym domänlogik{#anonymous-domain-logic}

## Domänregistreringslogik {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

Referensimplementeringen använder följande logik för anonym domänregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Söka efter domännamnet i `DomainServerInfo` tabell.
1. Om du inte hittar någon post infogar du en post i tabellen.

   Standardvärdena är:

   * `authentication is not required`
   * `no membership maximum`

   Om autentisering krävs för den begärda domänen kontrollerar du att det finns en giltig autentiseringstoken i begäran. Om autentiseringsnamnutrymmet anges i databasen måste token matcha det angivna autentiseringsnamnutrymmet.
1. Om autentisering krävs, men ingen giltig autentiseringstoken är tillgänglig, returnerar fel `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Kontrollera om enheten är registrerad i domänen:

   1. Söka efter domännamnet i `DomainMembership` tabell.
   1. Jämför det dator-GUID som du hittar med maskin-GUID i begäran.
   1. Om det här är en ny dator lägger du till en post i `DomainMembership` tabell.
   1. Om det är en ny enhet och `Max Membership` värdet har nåtts, returfel `DOM_LIMIT_REACHED (502)`.

1. Sök efter alla domännycklar för den här domänen i `DomainKeys` tabell:

   1. If `DomainServerInfo` anger att nycklarna måste rullas över och skapar ett nytt nyckelpar.
   1. Spara nyckelparet i `DomainKeys` tabell, med en nyckelversion som är en siffra högre än den högsta befintliga tangenten.
   1. Återställ `Key Rollover Required` flagga in `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

## Avregistreringslogik för domän {#section_C968BBFCBFAB4510A903D169F38C9FCE}

Referensimplementeringen använder följande logik för anonym domänavregistrering:

1. Tolka domännamnet från begärande-URL:en.
1. Sök efter det begärda domännamnet i `DomainServerInfo` tabell.
1. Om autentisering krävs för den begärda domänen kontrollerar du att det finns en giltig autentiseringstoken i begäran.

   Token måste också matcha det autentiseringsnamnutrymme som anges i databasen.
1. Slå upp domännamnet och datorns GUID i `DomainMembership` tabell.

   Om du inte hittar någon matchande post returneras felet `DEREG_DENIED (401)`.

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `DomainMembership`och in `DomainServerInfo`, ange `Key Rollover Required` flagga.

Eftersom ett stort antal datorer kan ansluta till domänen kan du inte matcha dator-ID:t. I stället tillämpas det slumpmässiga maskin-GUID som tilldelas datorn under personaliseringen.
