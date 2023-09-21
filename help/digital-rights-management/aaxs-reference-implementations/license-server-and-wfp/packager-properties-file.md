---
title: Packager properties file
description: Packager properties file
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Packager properties file {#packager-properties-file}

Använd [!DNL flashaccess-refimpl-packager.properties] -fil för att konfigurera den bevakade mapppaketerarkomponenten för referensimplementeringen. Du måste åtminstone ange licensserverns URL, licensserverns certifikat, paketerarens autentiseringsuppgifter och nyckelskyddsalternativ. Den här filen innehåller också platsen för varje bevakad mapp (packager.watchfolder.source). `n`). Alla ändringar som görs i värdena i den här egenskapsfilen börjar gälla nästa gång den bevakade mapppaketeraren körs (du behöver inte starta om servern). Om det finns ett konfigurationsfel i paketeraren avslutas den bevakade mapppaketerartråden och servern måste startas om för att starta om paketerartråden.
