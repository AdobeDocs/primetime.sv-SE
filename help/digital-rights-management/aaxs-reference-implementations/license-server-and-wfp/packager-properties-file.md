---
title: Packager-egenskapsfil
description: Packager-egenskapsfil
copied-description: true
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Packager-egenskapsfil {#packager-properties-file}

Använd [!DNL flashaccess-refimpl-packager.properties] -fil för att konfigurera den bevakade mapppaketerarkomponenten för referensimplementeringen. Du måste åtminstone ange licensserverns URL, licensserverns certifikat, paketerarens autentiseringsuppgifter och nyckelskyddsalternativ. Den här filen innehåller också platsen för varje bevakad mapp (packager.watchfolder.source). `n`). Alla ändringar som görs i värdena i den här egenskapsfilen börjar gälla nästa gång den bevakade mapppaketeraren körs (du behöver inte starta om servern). Om det finns ett konfigurationsfel i paketeraren avslutas den bevakade mapppaketerartråden och servern måste startas om för att starta om paketerartråden.
