---
title: Bevakade mappar
description: Bevakade mappar
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Bevakade mappar {#watched-folders}

Du kan använda Bevakade mappar för att automatiskt paketera innehåll som skapats i vissa mappar. Varje bevakad mapp kan konfigureras med olika paketeringsalternativ. Om du vill testa paketeringsalternativen innan du skapar en bevakad mapp använder du fliken Packa media.

Om du vill skapa en bevakad mapp klickar du på **[!UICONTROL Add New Watched Folder]** och fyll i förpackningsalternativen. Se [Paketera mediefiler](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md) för att få en beskrivning av varje alternativ. När du är klar klickar du **[!UICONTROL Save Watched Folder Properties]**.

När en bevakad mapp sparas sparas paketeringsalternativen i *[Indatamapp]* [!DNL \properties\watchfolder.properties]. Allt innehåll som läggs till i indatamappen och som uppfyller villkoren för val av indatamediefil paketeras automatiskt och placeras i utdatamappen. Se inställningarna för den globala bevakade mappen i avsnittet [Inställningar för Packager](../../aaxs-reference-implementations/fam-air-app-usage/initial-fam-setup-set-prefs/initial-fam-setup-pkg-prefs.md) om du vill konfigurera ytterligare alternativ för bevakad mapp.

Om du vill ändra inställningarna för Bevakade mappar väljer du indatasökvägen för Bevakade mappar i listan längst upp på skärmen. Ändra inställningarna och klicka på **[!UICONTROL Save Watched Folder Properties]**.

Om du vill ta bort en bevakad mapp väljer du indatasökvägen för bevakad mapp i listan högst upp på skärmen och klickar på **[!UICONTROL Delete Watched Folder Properties]**.
