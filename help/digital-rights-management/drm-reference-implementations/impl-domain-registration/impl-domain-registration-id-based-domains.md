---
title: Identitetsbaserad domänregistreringslogik
description: Identitetsbaserad domänregistreringslogik
copied-description: true
exl-id: 6e391fce-00b4-45cf-b785-3b0ec734a11e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Identitetsbaserad domänregistreringslogik{#identity-based-domain-registration-logic}

## Domänregistreringslogik {#section_149C247458954877AF158B4A09A8526B}

Referensimplementeringen använder följande logik för identitetsbaserad domänregistrering:

1. Avgör vilket domännamn som ska tilldelas till en angiven användare.

   Domännamnet ( `namequalifier:username`) extraheras från autentiseringstoken. Om ingen token är tillgänglig genereras ett fel.
1. Söka efter domännamnet i `DomainServerInfo` tabell.

   Om ingen post hittas infogar du en post. Standardvärdena är:

   * `authentication required`
   * `max domain membership=5`

   .

1. Så här verifierar du att enheten har registrerats i domänen:

   1. Slå upp `domainname` i `UserDomainMembership` tabell:

      1. För varje dator-ID som finns, jämför du ID:t med dator-ID:t i begäran.
      1. Om det här är en ny dator lägger du till en post i `UserDomainMembership` tabell.
      1. Sök efter matchande poster i `UserDomainRefCount` tabell.
      1. Lägg till en post om det inte finns någon post för det här maskin-GUID:t.
   1. Om det är en ny enhet, och `Max Membership` värdet har nåtts, returfel.


1. Sök efter alla domännycklar för den här domänen i `DomainKeys` tabell:

   1. If `DomainServerInfo` anger att nycklarna måste rullas över, skapar ett nytt nyckelpar,
   1. Spara paret i `DomainKeys` tabell, med en nyckelversion som är en högre än den högsta befintliga nyckeln.
   1. Återställ `Key Rollover Required` flagga in `DomainServerInfo`.

   1. Generera en domänautentiseringsuppgift för varje domännyckel.

## Avregistreringslogik för domän {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

Referensimplementeringen använder följande logik för identitetsbaserad domänavregistrering:

1. Avgör vilket domännamn som ska tilldelas den här användaren.

   Domännamnet är `namequalifier:username`, som extraheras från autentiseringstoken. Om ingen token är tillgänglig returneras felet `DOM_AUTHENTICATION_REQUIRED (503)` inträffar.
1. Sök efter det begärda domännamnet i `DomainServerInfo` tabell.
1. Söka efter domännamnet i `UserDomainMembership` tabell.
1. Jämför varje dator-ID som du hittar med dator-ID i begäran.
1. Leta reda på motsvarande post i `UserDomainRefCount` tabell.

   Om ingen matchande post hittas returneras ett fel.

1. Om detta inte är en förhandsgranskningsbegäran tar du bort posten från `UserDomainRefCount` tabell.
1. Om det inte finns några ytterligare poster i tabellen för datorn tar du bort posten från `UserDomainMembership` och ange [!DNL Key Rollover Required] flagga i `DomainServerInfo` -egenskap.

Varje användare kan registrera ett litet antal datorer så att du kan använda hela dator-ID:t och `matches()` metod för att räkna datorer. Eftersom en användare kan registrera flera gånger, via flera AIR-program eller spelare i olika webbläsare, måste servern behålla ett referensantal så att avregistreringen också kan räknas.

>[!NOTE]
>
>Avregistreringen är inte slutförd förrän alla domäntoken på datorn har återgetts.
