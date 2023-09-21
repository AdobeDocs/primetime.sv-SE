---
description: TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.
title: Bygg Primetimes referensimplementering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Bygg Primetimes referensimplementering {#build-the-primetime-reference-implementation}

TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.

Så här konfigurerar och skapar du Primetime Reference-projektet i Eclipse:

1. Ladda ned zip-filen för TVSDK Android och packa upp den i en katalog på en plats som du kommer ihåg.
1. Starta Eclipse.
1. Välj **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Välj **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Klicka **[!UICONTROL Next]**.
1. Använd **[!UICONTROL Browse]** för att fylla i **[!UICONTROL Root Directory]** fält med katalogen under [!DNL samples/PrimetimeReference/src] till vilken du packade upp TSDK Android zip-filen.
1. Välj följande projekt att importera: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Klicka **[!UICONTROL Finish]**.
1. Välj  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** för att bygga projektet.

   Det här steget är inte nödvändigt om projektet är konfigurerat att byggas automatiskt.
1. Om du vill inkludera testprojektet på arbetsytan kopplar du testprojektet till PrimetimeReference-projektet:
   1. Upprepa steg 3. till 6.
   1. Välj följande projekt att importera: `PrimetimeReference\tests`.
   1. Klicka **[!UICONTROL Finish]**.

      Testprojektet är beroende av CatalogActivity-projektet, så du måste associera testprojektet med CatalogActivity-projektet.
   1. Högerklicka **[!UICONTROL tests]** och välja **[!UICONTROL Properties]**.
   1. Välj **[!UICONTROL Projects]** under Java Build Path.
   1. Klicka **[!UICONTROL Add...]**
   1. Välj Katalogaktivitet.
   1. Klicka **[!UICONTROL OK]** för att lägga till projektet.
   1. Klicka **[!UICONTROL OK]** för att avsluta sidan Egenskaper.
   1. Välj  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** för att bygga projektet.

      Det här steget är inte nödvändigt om projektet är konfigurerat att byggas automatiskt.
