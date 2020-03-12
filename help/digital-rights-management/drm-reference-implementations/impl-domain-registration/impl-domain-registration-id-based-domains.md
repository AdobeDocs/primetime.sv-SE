---
description: 'null'
seo-description: 'null'
seo-title: Identitetsbaserad domänregistreringslogik
title: Identitetsbaserad domänregistreringslogik
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Identitetsbaserad domänregistreringslogik{#identity-based-domain-registration-logic}

## Domänregistreringslogik {#section_149C247458954877AF158B4A09A8526B}

Referensimplementeringen använder följande logik för identitetsbaserad domänregistrering:

1. Avgör vilket domännamn som ska tilldelas till en angiven användare.

   Domännamnet ( `namequalifier:username`) extraheras från autentiseringstoken. Om ingen token är tillgänglig genereras ett fel.
1. Slå upp domännamnet i `DomainServerInfo` tabellen.

   Om ingen post hittas infogar du en post. Standardvärdena är:

   * `authentication required`
   * `max domain membership=5`
   .

1. Så här verifierar du att enheten har registrerats i domänen:

   1. Slå upp `domainname` i `UserDomainMembership` tabellen:

      1. För varje dator-ID som finns, jämför du ID:t med dator-ID:t i begäran.
      1. Om det här är en ny dator lägger du till en post i `UserDomainMembership` tabellen.
      1. Sök efter matchande poster i `UserDomainRefCount` tabellen.
      1. Lägg till en post om det inte finns någon post för det här maskin-GUID:t.
   1. Om det är en ny enhet och `Max Membership` värdet har nåtts returnerar du ett fel.


1. Slå upp alla domännycklar för den här domänen i `DomainKeys` tabellen:

   1. Generera ett nytt nyckelpar om `DomainServerInfo` det indikerar att tangenterna måste rullas över,
   1. Spara paret i `DomainKeys` tabellen med en nyckelversion som är en högre än den högsta befintliga tangenten.
   1. Återställ `Key Rollover Required` flaggan i `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

## Avregistreringslogik för domän {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

Referensimplementeringen använder följande logik för identitetsbaserad domänavregistrering:

1. Avgör vilket domännamn som ska tilldelas den här användaren.

   Domännamnet är `namequalifier:username`, vilket extraheras från autentiseringstoken. Om ingen token är tillgänglig returneras ett fel `DOM_AUTHENTICATION_REQUIRED (503)` .
1. Leta upp det begärda domännamnet i `DomainServerInfo` tabellen.
1. Slå upp domännamnet i `UserDomainMembership` tabellen.
1. Jämför varje dator-ID som du hittar med dator-ID i begäran.
1. Leta reda på motsvarande post i `UserDomainRefCount` tabellen.

   Om ingen matchande post hittas returneras ett fel.

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `UserDomainRefCount` tabellen.
1. Om det inte finns några ytterligare poster i tabellen för datorn tar du bort posten från `UserDomainMembership` och anger [!DNL Key Rollover Required] flaggan i `DomainServerInfo` egenskapen.

Varje användare kan registrera ett litet antal datorer, så du kan använda det fullständiga dator-ID:t och metoden för att räkna datorer `matches()` . Eftersom en användare kan registrera flera gånger, via flera AIR-program eller spelare i olika webbläsare, måste servern behålla ett referensantal så att avregistrering också kan räknas.

>[!NOTE]
>
>Avregistreringen är inte slutförd förrän alla domäntoken på datorn har återgetts.

