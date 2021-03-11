---
title: Packager-egenskapsfil
description: Packager-egenskapsfil
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Packager properties file {#packager-properties-file}

Använd filen [!DNL flashaccess-refimpl-packager.properties] för att konfigurera komponenten Watched Folder Packager i referensimplementeringen. Du måste åtminstone ange licensserverns URL, licensserverns certifikat, paketerarens autentiseringsuppgifter och nyckelskyddsalternativ. Den här filen innehåller också platsen för varje bevakad mapp (packager.watchfolder.source). `n`). Alla ändringar som görs i värdena i den här egenskapsfilen börjar gälla nästa gång den bevakade mapppaketeraren körs (du behöver inte starta om servern). Om det finns ett konfigurationsfel i paketeraren avslutas den bevakade mapppaketerartråden och servern måste startas om för att starta om paketerartråden.
