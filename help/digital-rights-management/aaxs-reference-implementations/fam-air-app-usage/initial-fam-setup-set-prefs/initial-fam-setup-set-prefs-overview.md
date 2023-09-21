---
title: Översikt över inställningar
description: Översikt över inställningar
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Översikt över inställningar {#setting-preferences-overview}

Med undantag för Packager Server-URL:en lagras alla inställningar som anges nedan i [!DNL flashaccess-refimpl-packager.properties] på servern. Alla inställningar kan ändras antingen direkt i egenskapsfilen eller via AIR-programmet. Lösenord krypteras när de lagras i egenskapsfilen på servern. Skriv det okrypterade lösenordet i användargränssnittet, så krypteras det innan det lagras i filen.

>[!NOTE]
>
>Alla kataloger och sökvägar refererar till kataloger på paketerarservern, inte till klienten som kör AIR.

Alla ändringar som görs här börjar gälla omedelbart när inställningarna sparas. Servern behöver inte startas om om inte Packager-tråden avslutas på grund av konfigurationsproblem.

Inställningsbeskrivningarna använder följande termer:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Inställningar </th> 
   <th colname="2" class="- topic/entry entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL för Packager Server </td> 
   <td colname="2" class="- topic/entry "> Plats för servern som körs <span class="filepath"> flashaccess-packager.war </span>; till exempel <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Resurskatalog </td> 
   <td colname="2" class="- topic/entry "> Katalog som innehåller principer, certifikat, autentiseringsuppgifter och andra resurser som krävs för paketerarservern </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Licensserverns URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL för den server som klienten ska begära en licens från, till exempel <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>
