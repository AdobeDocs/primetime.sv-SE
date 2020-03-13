---
description: TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.
seo-description: TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.
seo-title: Bygg Primetimes referensimplementering
title: Bygg Primetimes referensimplementering
uuid: ab12660a-1563-49a4-82d9-1ab13f8a92be
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Bygg Primetimes referensimplementering {#build-the-primetime-reference-implementation}

TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.

Så här konfigurerar och skapar du Primetime Reference-projektet i Eclipse:

1. Ladda ned zip-filen för TVSDK Android och packa upp den i en katalog på en plats som du kommer ihåg.
1. Starta Eclipse.
1. Välj **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Välj **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Klicka på **[!UICONTROL Next]**.
1. Använd **[!UICONTROL Browse]** knappen för att fylla i **[!UICONTROL Root Directory]** fältet med katalogen under [!DNL samples/PrimetimeReference/src] vilken du packade upp TSDK Android-zip-filen.
1. Välj följande projekt att importera: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**..
1. Klicka på **[!UICONTROL Finish]**.
1. Välj **[!UICONTROL Project]** > **[!UICONTROL Build Project]** för att skapa projektet.

   Det här steget är inte nödvändigt om projektet är konfigurerat att byggas automatiskt.
1. Om du vill inkludera testprojektet på arbetsytan kopplar du testprojektet till PrimetimeReference-projektet:
   1. Upprepa steg 3. till 6.
   1. Välj följande projekt att importera: `PrimetimeReference\tests`.
   1. Klicka på **[!UICONTROL Finish]**.

      Testprojektet är beroende av CatalogActivity-projektet, så du måste associera testprojektet med CatalogActivity-projektet.
   1. Högerklicka **[!UICONTROL tests]** och välj **[!UICONTROL Properties]**.
   1. Välj fliken **[!UICONTROL Projects]** under Java Build Path.
   1. Klicka på **[!UICONTROL Add...]**
   1. Välj Katalogaktivitet.
   1. Klicka **[!UICONTROL OK]** för att lägga till projektet.
   1. Klicka **[!UICONTROL OK]** för att stänga sidan Egenskaper.
   1. Välj **[!UICONTROL Project]** > **[!UICONTROL Build Project]** för att skapa projektet.

      Det här steget är inte nödvändigt om projektet är konfigurerat att byggas automatiskt.
