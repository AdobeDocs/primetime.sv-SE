---
description: TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.
title: Bygg Primetimes referensimplementering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---


# Bygg implementeringen av Primetime-referensen {#build-the-primetime-reference-implementation}

TVSDK Primetime Reference är en Android-applikation som byggts runt ramverken TVSDK och AVE.

Så här konfigurerar och skapar du Primetime Reference-projektet i Eclipse:

1. Ladda ned zip-filen för TVSDK Android och packa upp den i en katalog på en plats som du kommer ihåg.
1. Starta Eclipse.
1. Välj **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Välj **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Klicka på **[!UICONTROL Next]**.
1. Använd knappen **[!UICONTROL Browse]** för att fylla i fältet **[!UICONTROL Root Directory]** med katalogen under [!DNL samples/PrimetimeReference/src] som du packade upp TSDK Android-zip-filen till.
1. Välj följande projekt att importera: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Klicka på **[!UICONTROL Finish]**.
1. Välj **[!UICONTROL Project]** > **[!UICONTROL Build Project]** för att skapa projektet.

   Det här steget är inte nödvändigt om projektet är konfigurerat att byggas automatiskt.
1. Om du vill inkludera testprojektet på arbetsytan kopplar du testprojektet till PrimetimeReference-projektet:
   1. Upprepa steg 3. till 6.
   1. Välj följande projekt att importera: `PrimetimeReference\tests`.
   1. Klicka på **[!UICONTROL Finish]**.

      Testprojektet är beroende av CatalogActivity-projektet, så du måste associera testprojektet med CatalogActivity-projektet.
   1. Högerklicka på **[!UICONTROL tests]** och välj **[!UICONTROL Properties]**.
   1. Välj fliken **[!UICONTROL Projects]** under Java Build Path.
   1. Klicka på **[!UICONTROL Add...]**
   1. Välj Katalogaktivitet.
   1. Klicka på **[!UICONTROL OK]** för att lägga till projektet.
   1. Klicka på **[!UICONTROL OK]** för att avsluta sidan Egenskaper.
   1. Välj **[!UICONTROL Project]** > **[!UICONTROL Build Project]** för att skapa projektet.

      Det här steget är inte nödvändigt om projektet är konfigurerat att byggas automatiskt.
