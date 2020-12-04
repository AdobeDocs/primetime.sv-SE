---
seo-title: Packager-egenskapsfil
title: Packager-egenskapsfil
uuid: 156624ec-66f0-4718-8a66-ed04a47f234d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Packager properties file {#packager-properties-file}

Använd filen [!DNL flashaccess-refimpl-packager.properties] för att konfigurera komponenten Watched Folder Packager i referensimplementeringen. Du måste åtminstone ange licensserverns URL, licensserverns certifikat, paketerarens autentiseringsuppgifter och nyckelskyddsalternativ. Den här filen innehåller också platsen för varje bevakad mapp (packager.watchfolder.source). `n`). Alla ändringar som görs i värdena i den här egenskapsfilen börjar gälla nästa gång den bevakade mapppaketeraren körs (du behöver inte starta om servern). Om det finns ett konfigurationsfel i paketeraren avslutas den bevakade mapppaketerartråden och servern måste startas om för att starta om paketerartråden.
