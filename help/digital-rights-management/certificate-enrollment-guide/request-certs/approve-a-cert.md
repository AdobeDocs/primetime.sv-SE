---
description: 'null'
seo-description: 'null'
seo-title: Godkänn ett certifikat (konto eller sekundär administratör)
title: Godkänn ett certifikat (konto eller sekundär administratör)
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Godkänn ett certifikat (konto eller sekundär administratör){#approve-a-certificate-account-or-secondary-administrator}

1. Logga in på webbplatsen för certifikatregistrering.
1. Välj fliken **[!UICONTROL Certificates]**.
1. Granska begäran för att verifiera att den är giltig.
1. Om begäran är giltig klickar du på **[!UICONTROL Approve]**.

   Du kan också lägga till en kommentar. Ett e-postmeddelande skickas till den begärande parten som anger att begäran har godkänts av en av företagsadministratörerna. En kopia av det här e-postmeddelandet skickas till företaget och Adobe-administratörerna.

1. Om begäran inte är giltig klickar du på **[!UICONTROL Reject]** och anger en kommentar i bekräftelsedialogrutan.

   Ett e-postmeddelande skickas till den begärande parten som anger att begäran har avvisats av en av företagsadministratörerna. En kopia av det här e-postmeddelandet skickas till företagsadministratörerna.

När en administratör godkänner en certifikatbegäran verifierar Adobe identiteten för den begärande. Adobe kontaktar den begärande parten via det telefonnummer som anges i deras profil.

Administratören i Adobe försöker kontakta den begärande parten två gånger inom en tredagarsperiod. Om Adobe-administratören inte kan kontakta den begärande parten lämnar de ett meddelande där de begär ett återanrop eller anger en tidpunkt när de ska ringa igen. Om Adobe-administratören inte kan nå den begärande parten skickas ett e-postmeddelande till administratörerna.

>[!NOTE]
>
>Det är bara kontoadministratören och den sekundära administratören som kan ändra företagets telefonnummer och bestridande fras för beställaren.

Om identiteten för den begärande parten verifieras får den begärande parten ett e-postmeddelande som innehåller PKCS#7-filen ( [!DNL p7b]).

Beställaren kan kopiera PKCS#7-innehållet från e-postmeddelandet och spara det i en fil eller använda den fil som är bifogad i e-postmeddelandet. Adobe rekommenderar att du när du sparar PKSC#7-filen använder basnamnet som du använde för att generera den privata nyckeln och CSR-filen.

>[!NOTE]
>
>Filen som skickades till den begärande innehåller bara certifikatet. Filen innehåller ingen information om privat nyckel.

