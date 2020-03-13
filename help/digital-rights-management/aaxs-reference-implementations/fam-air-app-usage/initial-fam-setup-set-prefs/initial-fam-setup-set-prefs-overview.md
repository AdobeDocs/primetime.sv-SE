---
seo-title: Översikt över inställningar
title: Översikt över inställningar
uuid: d1c067b1-6c2b-460e-8d00-5a5bfee0789c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Översikt över inställningar {#setting-preferences-overview}

Med undantag för Packager Server-URL:en lagras alla inställningar som anges nedan i [!DNL flashaccess-refimpl-packager.properties] filen på servern. Alla inställningar kan ändras antingen direkt i egenskapsfilen eller via AIR-programmet. Lösenord krypteras när de lagras i egenskapsfilen på servern. Skriv det okrypterade lösenordet i användargränssnittet, så krypteras det innan det lagras i filen.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Alla kataloger och sökvägar refererar till kataloger på paketerarservern, inte på klienten som kör AIR-programmet.

Alla ändringar som görs här börjar gälla omedelbart när inställningarna har sparats. Servern behöver inte startas om om inte Packager-tråden avslutas på grund av konfigurationsproblem.

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
   <td colname="2" class="- topic/entry "> Plats för server som kör <span class="filepath"> flashaccess-packager.war </span>. till exempel <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Resurskatalog </td> 
   <td colname="2" class="- topic/entry "> Katalog som innehåller principer, certifikat, autentiseringsuppgifter och andra resurser som krävs för paketerarservern </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Licensserverns URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL för den server från vilken klienten ska begära en licens. till exempel <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

