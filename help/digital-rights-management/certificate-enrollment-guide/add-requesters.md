---
title: Lägg till beställare
description: Lägg till beställare
copied-description: true
exl-id: 66d9bc90-8287-4a07-9f60-4263888d5cce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Lägg till beställare{#add-requesters}

En Adobe Primetime DRM-licenstagare kan ha upp till fem beställare. Adobe råder er dock att begränsa antalet beställare till de personer som utvecklar Primetimes DRM-lösning. Begärarna ansvarar för att lagra den privata nyckeln på en säker plats.

1. En administratör loggar in på webbplatsen för certifikatregistrering med en giltig Adobe ID som innehåller licensinnehavarens domännamn.
1. På startsidan klickar du på **[!UICONTROL Add a Requester]**.
1. På fliken Användarkonton gör du *en* av följande:

   * Lägg till användare.

      Om medarbetaren har ett Adobe-konto anger du e-postadressen. Klicka **[!UICONTROL Add]** och fortsätta.
   * Bjud in användare.

      Om medarbetaren inte har något Adobe-konto kan du bjuda in dem att skapa ett. Ange medarbetarens e-postadress och namn och klicka på **[!UICONTROL Send an invitation]**. Webbplatsen skickar en e-postinbjudan till den inbjudna. E-postmeddelandet innehåller en länk till adobe.com där mottagaren kan skapa ett konto. Mottagaren måste använda den e-postadress som inbjudan skickades till.

      >[!NOTE]
      >
      >Administratören får inget meddelande när en användare har skapat ett konto. Kontrollera **[!UICONTROL User accounts]** på webbplatsen för certifikatregistrering för att se om en inbjudare har skapat ett konto.

1. Om du har lagt till en användare visas rollavsnittet i **[!UICONTROL User accounts]** -fliken öppnas. Gör följande:

   1. Kontrollera att användarens information är korrekt.
   1. Ange företagets telefonnummer och svarsfras.

      Användaren måste känna till den här frasen för att kunna verifiera sitt konto.
   1. För användartyp väljer du **[!UICONTROL Requester]**.
   1. Klicka på Spara.

      Den begärande parten får ett e-postmeddelande om att deras DRM-kontoregistrering för Primetime har slutförts.

1. Om du har bjudit in en användare gör du följande:

   1. Logga in på webbplatsen för certifikatregistrering.
   1. Välj **[!UICONTROL User accounts]** -fliken.
   1. Hitta användaren i **[!UICONTROL Invitations Sent]** och klicka **[!UICONTROL Authorize]**.

      >[!NOTE]
      >
      >Om det inte finns en **[!UICONTROL Authorize]** i **[!UICONTROL Actions]** -kolumnen har den inbjudne inte skapat något Adobe-konto än.

   1. Bekräfta att beställarens information är korrekt.
   1. Ange företagets telefonnummer och svarsfras.

      Begäraren måste känna till den här frasen för att kunna verifiera sitt konto.
   1. För användartyp väljer du **[!UICONTROL Requester]**.
   1. Klicka **[!UICONTROL Save]**.

      Användaren får ett e-postmeddelande om att registreringen av deras Primetime DRM-konto har slutförts.
