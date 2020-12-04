---
seo-title: Information om NATIVE_ERROR-meddelandet
title: Information om NATIVE_ERROR-meddelandet
uuid: 750ee0e2-15d4-4602-9574-94015a6e1b57
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '6888'
ht-degree: 2%

---


# Information om NATIVE_ERROR-meddelandet {#details-for-the-native-error-notification}

När TVSDK hanterar ett systemspecifikt fel returneras några eller alla följande metadatanyckelvärden som strängar.

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Namn på metadatanyckel </th> 
   <th colname="col2" class="entry"> Metadatavärde </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>Inbyggd felkod från AVE. </p> <p>Dessa koder representerar följande: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM-fel (koderna 3300 till 3367). Detta är samma som motsvarande felkoder för Flash Player </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Videouppspelningsfel (-1 till 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Kryptografifel (300 till 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">Kort beskrivning av meddelandet (till exempel <span class="codeph"> AAXS_InvalidVoucher</span> eller <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> BESKRIVNING</span> </td> 
   <td colname="col2"> Lång beskrivning av meddelandet (t.ex. Ad resolving operation has failed). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodenumeric-värde som en sträng (till exempel"13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.</span> PSDKErrorCodeas a string (till exempel  <span class="codeph"> kECNetworkError</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> VARNING</span> </td> 
   <td colname="col2"> Beskrivning av varningen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> FEL</span> </td> 
   <td colname="col2"> Beskrivning av felet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> Mindre fel från DRM-modulen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> Beskrivning av felet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> URL för den DRM-server som TVSDK försökte prata med. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Inläsningsfel för annonsmanifestet</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL för innehållet som inte kunde läsas in. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Typ av annons (en konstant från uppräkningen <span class="codeph"> MediaResource.Type</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> Annonsens längd i millisekunder. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> ID som tilldelats annonsen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Filfel</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> Beskrivning av felet vid hämtning av mediefiler. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> URL till filen som hämtas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> Beskrivning av fel vid hämtning av manifestfil. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Beskrivning av fel under hämtning av fragment (till exempel <span class="codeph"> ts</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Fel i ljudspår</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Namnet på ljudspåret som inte kunde läsas in, enligt specifikationen i manifestet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> Ljudspårets språk, enligt specifikationen i manifestet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Sök efter fel</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> ID för perioden (heltal). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>Positionen (i millisekunder) sökdes (dubbel). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Diverse</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Auditude-felkod (nummer). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: DRM-värden {#section_D240082B93D34902A18C3923C1C717B3}

Videomodulens Video Encoder-gränssnitt returnerar dessa DRM-meddelanden i metadataobjektet `NATIVE_ERROR`.

När du rapporterar DRM-fel till Adobe måste du inkludera `NATIVE_SUBERROR_CODE` och `DRM_ERROR_STRING` för felsökningshjälp.

>[!TIP]
>
>Den här listan innehåller TVSDK-specifik information om felen. Fullständiga beskrivningar finns i [ActionScript-referens för körningsfel i ActionScript för Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Värde för metadatanyckeln NATIVE_- ERROR_CODE </th> 
   <th colname="col2" class="entry"> Värde för metadatanyckeln NATIVE_ERROR_NAME </th> 
   <th colname="col3" class="entry"> Betydelse </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">Vad distributörens programvara ska göra: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Om du använder Google Chrome och är i Incognito-läge och din Flash Player-version är mindre än 11.6 kan det här felet uppstå. <p>Vi rekommenderar att spelaren kontrollerar webbläsarens versionsnummer och råder användaren att avsluta Incognito-läget. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Begär licensen igen. <p>Om begäran lyckas behöver du inte logga eller eskalera. Om begäran misslyckas loggar du det innehåll som orsakade felet. <span class="codeph"> </span> subErrorId innehåller ett radfel om ett sådant finns. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">Vad distributören ska göra: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Om nya försök misslyckas på andra konfigurationer än Chrome med Flash som är mindre än version 11.6 kan ett fel ha uppstått i förpackningen. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Kontrollera om problemet är specifikt för visst innehåll och ompackning. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>Servern kunde inte autentisera eller auktorisera klienten. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">Distributörens programvara ska vidta alla åtgärder som krävs för att återupprätta användarens inloggningsuppgifter eller vägleda användaren till att få åtkomst till innehållet. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">Distributören bör bekräfta att distributörens autentiserings- och autentiseringsmekanism fungerar korrekt. <p>Om distributörerna inte planerar att använda autentiserings- eller auktoriseringsfunktionerna bör de kontrollera om policyn för det felaktiga innehållet kräver autentisering och se Diagnostiseringspolicy/licensavvikelser. </p> </li> 
    </ul> <p>Mer information om den här felkoden finns i <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM-fel 3301 - orsaker och upplösning</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>I Access 4.0 och senare genereras det här felet på iOS när URL:en för fjärrnyckeln inte använder HTTPS som schema. HTTPS krävs. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">Om distributören använder en version som är äldre än Access v4, eller version minst 4 men plattformen inte är iOS, bör distributörens programvara logga felet. <p>Felet genereras bara på iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">Om distributörens programvara är minst Adobe Access version 4 och plattformen är iOS, måste distributörerna ändra fjärrnyckelserverns URL som de använder till HTTPS. <p>Om de bara använder HTTP kan distributörerna behöva konfigurera en HTTPS-server. I annat fall måste distributörerna skicka den loggade informationen till Adobe och eskalera problemet. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>Innehållet som du visar har upphört att gälla enligt reglerna som angetts av innehållsleverantören. subErrorId innehåller ett klientspecifikt fel eller radfel. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">Distributörens programvara ska försöka återhämta licensen från servern en gång för att avgöra om det finns en ny licens som inte har gått ut. <p>Om ingen licens är tillgänglig eller om licensen har gått ut, tillåt användaren att skaffa en ny licens eller informera användaren om att innehållet inte kan bevakas.Om innehållet har paketerats med en princip som har ett förfallodatum/slutdatum, rapporterar licensservern ett <span class="codeph"> PolicyEvaluationException</span> och anger att principens slutdatum har gått ut (serverfelkod 303). Kontrollera serverns loggfiler som ska verifieras. </p> <p>Om det är möjligt bör kunderna kontrollera vilken policy de använde vid paketeringen för att se om den har upphört att gälla. Java-kommandoradsverktyget är: 
        <code>
         java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol
        </code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">Distributören bör bekräfta om licensens förfallodatum är konfigurerade som avsett. </li> 
     </ul> </p> <p>Mer information om den här felkoden finns i <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Innehållet har upphört att gälla) med AMS/FMS som använder en direktström?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">Mer information om den här felkoden finns i <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM-fel 3301 - orsaker och upplösning</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>Anslutningen till licensen eller domänservrarna nådde en tidsgräns, antingen på grund av nätverksfördröjning eller på grund av att klienten är offline. I vanliga fall innehåller subErrorId HTTP-returkod. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">Distributörens programvara ska försöka upprätta en nätverksanslutning till en känd bra server. <p>Om försöket misslyckas ber du användaren att återansluta till nätverket. Om försöket lyckas loggar du det. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">Distributören bör kontrollera att alla licenser och domänservrar som används är online och synliga från klientens nätverk. </li> 
    </ul> <p>Mer information om den här felkoden finns i <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] reason and resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Använd en nyare version av TVSDK för Android. <p>Den aktuella klienten kan inte slutföra den begärda åtgärden, men en uppdaterad klient kan eventuellt slutföra begäran. </p> <p>Detta kan ha flera orsaker: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">En delad domän användes som inte är tillgänglig på den här klienten. Detta är troligtvis fallet när uppspelningen fungerar i Chrome, men inte i någon annan webbläsare och vice versa. <p> <p>Tips: Chrome använder en annan PHDS/PHLS-nyckel än de andra webbläsarna. Mer information finns i <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">Programmet försöker lägga till flera DRMS-sessioner när det körs på en iOS-version som är tidigare än 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">Metadata har version 3 eller senare när endast version 2 stöds. </li> 
     </ul> </p> 
    <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
     <li id="li_7A83869D4262443DA35FA1DF8D3097DD">Distributörens programvara ska varna användaren och avbryta åtgärden. <p>Om programmet har ett sätt att avgöra om en uppgradering är tillgänglig kan du hänvisa användaren till uppgraderingen på lämpligt sätt för plattformen. </p> </li> 
     <li id="li_AF9C2711FDE54DA196EB9D2864632000">Om problemet uppstår på grund av en delad domän måste distributören kontrollera med Adobe om det finns en uppdaterad körningsversion eller bibliotek. <p>För Flash-miljön kan distributören framtvinga uppgraderingen direkt i programmet. Om det är ett bibliotek måste distributören skaffa ett uppdaterat bibliotek, bygga om programmet och distribuera det till användarna. </p> <p>Om problemet uppstår på grund av flera DRMSessions måste distributören uppdatera sitt program för att kontrollera iOS-versionsnumret innan flera DRMS-sessioner läggs till. Eller så kan de begränsa distributionen av sina program till iOS v5 och senare. </p> <p>om problemet inträffar på grund av att metadataversionen är högre än version 2 är problemet antagligen skadade metadata. De kan försöka återskapa metadata och se resultaten. Om de fortsätter att se problemet loggar de in och eskalerar till Adobe. </p> </li> 
    </ul> <p>Mer information om den här felkoden finns i <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> Så här åtgärdar du en 3306 DRMErrorEvent-felkod</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>Detta representerar vanligtvis ett fel i Adobe Access-koden och är oväntat, såvida det inte finns ett känt fel, som framgår nedan. subErrorId innehåller ett klientspecifikt fel eller radfel. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">Om webbläsaren är Chrome i Windows och Flash version är 11.6 (SWF version 19 eller senare), ska distributörens program anta att användaren tryckte på <span class="uicontrol"> Neka</span> i informationsfältet och behandla det som en 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">Om 3307 inträffar när webbläsaren inte är Chrome eller Flash inte är 11.6 bör distributören eskalera till Adobe. </li> 
    </ul> <p>Viktigt: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> kan inträffa med webbläsarversionerna 24-28 för Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>Det här felet inträffar när den licens som används innehåller fel nyckel för att dekryptera innehållet. subErrorId innehåller ett klientspecifikt fel eller radfel. </p> <p>Det finns bara två sätt att generera det här felet: 
     <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
      <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">Kunden har ändrat standardverktygen för Adobe för att generera licenser (till exempel agentserverns Java-ramverk). <p>I det här fallet innehåller licensen en felaktig nyckel som kanske inte motsvarar något innehåll. </p> </li> 
      <li id="li_21D04ED1F1FA464785BC297D385766FF">Kunden har utfärdat flera licenser med samma licens-ID. <p>I det här fallet finns det flera tillgängliga licenser på klienten som matchar innehållets metadata och Access-koden har valt fel för användning. </p> </li> 
     </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">Distributörens programvara ska försöka återhämta licensen från servern. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">Om ingen licens är tillgänglig eller om licensen har gått ut, ska du tillhandahålla ett arbetsflöde där användaren kan hämta en ny licens eller informera användaren om att innehållet inte kan bevakas och logga problemet. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">Om det här var ett domänbundet innehåll (för AIR) ska du ange ett sätt för användaren att ansluta till domänen. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">Distributören bör 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Kontrollera att de inte har skräddarsytt licensserverns licensutfärdandedelar. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Kontrollera att de utfärdar unika licens-ID:n för alla licenser. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Eskalera problemet med Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader  </span> </td> 
   <td colname="col3"> <p>Detta inträffar om sidhuvudet är större än 65536 byte. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">Distributörens programvara ska logga vilket innehåll som orsakade felet. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">Distributören bör bekräfta att felet kan reproduceras med specifika innehållsdelar. Paketera om brutet innehåll. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch  </span> </td> 
   <td colname="col3">Android-programmet matchar inte det som används. <p>Rätt AIR-program eller Flash SWF används inte. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch  </span> </td> 
   <td colname="col3"> Används inte. Problemet kan fortfarande genereras av version 1.x-stacken i AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity  </span> </td> 
   <td colname="col3"> Åtgärda problemet genom att ladda ned licensen på nytt från servern. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed  </span> </td> 
   <td colname="col3"> <p>Problemet inträffar när systemet inte kan skriva till filsystemet. <span class="codeph"> subErrorId </span> innehåller ett klientspecifikt fel eller radfel. </p> <p>I Microsoft Windows kan fel 3313 genereras av Active X- eller NPAPI-plug-in-flash-spelaren när det krypterade innehållet har ett licens-ID eller ett policy-ID som är för långt. Detta beror på den maximala sökvägslängden i Windows. (Plugin-programmet Pepper har inte det här problemet.) </p> <p>Se bevakning 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">Distributörens programvara ska uppmana användaren att bekräfta att användarens användarkatalog inte är låst eller på en volym som är full eller låst. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">Om distributören använder AIR, i stället för Flash, kan problemet bero på en begränsning av sökvägslängden. <p>Distributörerna bör förkorta namnet på AIR-programmet till något rimligt. Publicera också innehållet igen med ett kortare licens-ID<span class="codeph"> och ett <span class="codeph"> policy-ID</span>.</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata  </span> </td> 
   <td colname="col3"> <p>Det här felet indikerar ofta att innehållet paketerades med PKI-certifikat för testning, och spelaren byggs med PKI för produktion eller vice versa. subErrorId innehåller ett klientspecifikt fel eller radfel. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">Distributörens programvara ska logga vilket innehåll som orsakade felet. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">Distributören bör bekräfta att felet kan reproduceras med specifika innehållsdelar. <p>Du kanske måste paketera om brutet innehåll. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied  </span> </td> 
   <td colname="col3"> <p>Det finns kända fel där den här felkoden genereras när 3305 är avsedd. Mer information finns i <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] - orsaker och upplösning</a>. </p> <p>Fjärr-SWF som läses in av AIR har inte åtkomst till Flash Access-funktioner. Den här felkoden kan också genereras om ett säkerhetsfel inträffar under nätverksåtkomst. Exempel är om målservern inte ansluter klienten med crossdomain.xml, eller så går det inte att nå crossdomain.xml. </p> <p>Mer information finns i <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM-fel 3315 - möjlig rotorsak och upplösning</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED  </span> </td> 
   <td colname="col3"> Var <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModul</span>. Flyttad till 3344 på grund av en konflikt med felkoden för Flash. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFedlade  </span> </td> 
   <td colname="col3"> <p>Viktigt:  Detta är ett sällsynt fel och inträffar vanligtvis inte i en produktionsmiljö. </p> <p>Om felet inträffar kan du göra något av följande: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">Installera om AIR om du använder AIR. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Om du använder Flash Player hämtar du <span class="codeph"> AdobeCP</span>-modulerna igen. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion  </span> </td> 
   <td colname="col3"> Gäller inte för Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI  </span> </td> 
   <td colname="col3"> Gäller inte för Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed  </span> </td> 
   <td colname="col3"> Gäller inte för Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15nMisslyckades  </span> </td> 
   <td colname="col3"> <p>Det gick inte att etablera klienten med nycklar. subErrorId innehåller ett klientspecifikt, serverspecifikt eller radfel. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">Distributörens programvara bör försöka utföra åtgärden igen minst en gång. <p>Om du använder Google Chrome i Windows kan du förklara hur du tillåter plugin-åtkomst som inte finns i en sandlåda. Mer information finns i <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome's unsandbox access deny</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">Distributören ska utföra någon av följande uppgifter: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">Om felet är konsekvent mellan olika plattformar bör du eskalera problemet med Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Om felet är begränsat till Chrome i Windows vägleder du användaren till att tillåta åtkomst till obegränsat plugin-program. </li> 
      </ul> <p>Distributörerna bör uppdatera sin SWF-fil till version 19 eller senare och det Chrome-specifika 3321-felet uppstår ett 3368-fel. Fel 3368 kan hanteras mer specifikt av distributörens programvara. Den här ändringen introducerades i Chrome Stable Channel version 26.0.1410.43. </p> <p>Tips: Fel <span class="codeph"> 3321:1090519056</span> kan inträffa med Flash Player version 11.1 till 11.6. Vi rekommenderar att du uppgraderar till den senaste Flash Player-versionen. </p> </li> 
    </ul> <p>Mer information finns i <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM-fel 3321 Orsaker och upplösning</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Skadningsfel i Global Store</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed  </span> </td> 
   <td colname="col3"> <p>Enheten verkar inte matcha konfigurationen som fanns när den initierades. subErrorId innehåller ett klient- eller radfel. </p> <p>Distributörens programvara ska utföra någon av följande uppgifter: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>Om enheten inte använder Flash Player och använder AIR, iOS och så vidare, anropar du <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>Om problemet uppstår på iOS i en utvecklingsfas ber du utvecklaren att bekräfta om problemet uppstår när du växlar mellan byggen som har hämtats från tredjepartssystem för distribution före lansering (till exempel HockeyApp) och en lokal build från Xcode. Attribut för en tidigare installation skrivs inte över helt när du växlar mellan en build som distribuerats från HockeyApp och en build från Xcode. Den här situationen kan utlösa felet 3322. </p> <p>För att lösa det här problemet bör utvecklaren ta bort den äldre versionen från enheten innan den nya versionen installeras. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">Om enheten använder Flash Player, och den inte kan användas från felkoderna 3322 eller 3346, läser du instruktionerna från Adobe om hur du återställer DRM-licensarkivet programmatiskt på <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> DRM-fel 3322/3346/3368 i Chrome (Info-Bar Problems)</a>. </li> 
     </ul> </p> <p>Detta fel förväntas inte inträffa ofta. I företagsmiljöer där centrala profiler används ökar risken för att fel 3322 inträffar när användaren loggar in från olika datorer om en användare visar innehåll som skyddas av DRM. Distributören bör om möjligt försöka hämta informationen från användaren. </p> <p>Om felet inträffar ofta eskalerar du till Adobe. Du måste meddela Adobe om återställningen av licensarkivet lyckades lösa problemet och ange för Adobe vilka webbläsare felet inträffar. </p> <p>Mer information finns i följande artiklar: 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore  </span> </td> 
   <td colname="col3"> <p>Filer som används av DRM-klienten har oväntat ändrats. subErrorId innehåller ett klient- eller radfel. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">Distributörens programvara bör vägleda användaren till återställning på samma sätt som för 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">Om GlobalStore misslyckas i en högre hastighet än den förväntade felfrekvensen för hårddiskarna i din användarbas eskalerar du problemet till Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid  </span> </td> 
   <td colname="col3"> Återställ lokal DRM-lagring för det här programmet. Anropa DRMManager.resetDRM. <p>Licensservern kanske inte kan ansluta till CRL-servern (Certificate Revocation List) för att uppdatera sina CRL-filer, eller så begär klientdatorn en licens/autentisering som har återkallats av licensservern. </p> <p>I serverloggarna är felkoden 111 MachineTokenInvalid. På klientnivå översätts felkod 111 till felkod 3324. </p> <p>DRM-licensserveradministratören bör kontrollera om kundens licensserver någonsin har kunnat hämta Adobe CRL-filer. Om kunden använder Tomcat kan kunden kontrollera katalogen<span class="filepath"> tomcat/temp/</span> för att se om det finns 4 CRL-filer. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
     <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">Om filerna finns i den här katalogen dubbelklickar du på filerna i Utforskaren i Windows och i CRL-visningsprogrammet för att avgöra om någon av filerna har gått ut. </li> 
     <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">Om det inte finns några filer i tomcat/temp/ kan det förutsättas att den här licensservern aldrig har kunnat nå Adobe CRL-servern på grund av ett brandväggs-/routningsproblem. </li> 
    </ul> <p>Mer information finns i <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> Brandväggsregler</a>. </p> <p>Om CRL-filerna inte är tillgängliga eller har gått ut måste du bekräfta om licensservern kan nås. Öppna en nätverkssniffer på kundens licensserver, starta om servern och be en klient begära en licens från servern. Du kan observera nätverkstrafiken för att se om anrop till följande URL-slutpunkter lyckas: <p>Tips:  Du kan också ange följande URL-adresser för listor över återkallade certifikat i en webbläsare för att se om du kan hämta varje fil manuellt. </p> 
     <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
     </ul> </p> <p>Om brandväggsreglerna är öppna och det inte finns några aktuella 3324-fel kan det ha uppstått ett tillfälligt nätverksproblem. Kontrollera kundens serverloggar, som troligtvis finns i katalogen <span class="codeph"> /tomcat/logs/</span>, för att avgöra om ett fel uppstod när licensservern försökte hämta listan över återkallade certifikat. <p>Viktigt:  Ett fel kan uppstå när ett stort antal (eller en explosion) klienter rapporterar ett 3324-fel till ett tillfälligt nätverksproblem när en CRL-fil förnyas. När nätverksproblemet löstes löstes även 324 problem. </p> </p> <p>Om alla fyra CRL-filerna finns i katalogen <span class="filepath"> tomcat/temp/</span>, och klienterna fortfarande får 3324-felkoder, kan det uppstå problem med filåtkomst till CRL-filerna. För att lösa det här problemet kanske du vill granska loggarna och rensa de befintliga CRL-filerna. </p> <p>Om det inte finns några serverproblem ber du användaren att återställa enligt beskrivningen i 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Fel i serverarkivet</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore  </span> </td> 
   <td colname="col3"> <p>Filer som används av DRM-klienten har oväntat ändrats. <span class="codeph"> subErrorId </span> innehåller ett klient- eller radfel. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">Distributörens programvara bör försöka utföra åtgärden igen eftersom AdobeCP har tagit bort det felaktiga serverarkivet internt och ett nytt försök bör lyckas. Logga problemet om ett nytt försök misslyckas. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">Om nya försök misslyckas i en högre hastighet än den förväntade felfrekvensen för hårddiskarna i din användarbas eskalerar du problemet till Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected  </span> </td> 
   <td colname="col3"> Anropa <span class="codeph"> DRMManager.resetDRM</span>. <p>Licensarkivet har manipulerats/skadats och kan inte längre användas. </p> <p>Distributörens programvara bör vägleda användaren till återställning på samma sätt som beskrivs i 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected  </span> </td> 
   <td colname="col3"> Åtgärda klockan eller skaffa <span class="codeph"> licens för Authn/Lic/Domain</span> igen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Fel i autentisering/licens/domänserver</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryIgen  </span> </td> 
   <td colname="col3"> <p>Det här är ett fel på serversidan där servern inte kunde slutföra klientens begäran. Det här felet kan inträffa när servern till exempel är upptagen, HTTP/500, servern inte har den nyckel som krävs för att dekryptera begäran och så vidare. </p> <p>På klienten går det inte att avgöra vad som gick fel. Kunden måste granska Adobe Access-serverloggarna, som vanligtvis kallas <span class="codeph"> AdobeFlashAccess.log</span>, för att avgöra vad som gick fel. Det finns alltid en beskrivande stackspårning i loggen som indikerar problemet. <span class="codeph"> subErrorId </span> innehåller ett serverspecifikt fel eller radfel. </p> <p>Distributören bör titta i serverloggarna för att identifiera vilken server som skickar det här felet. För 3328-fel med underfelkod 101 kan servern inte dekryptera begäran. Kunden måste validera att de licens-/transportservercertifikat som är installerade på licensservern matchar och motsvarar de certifikat som används vid paketeringen. </p> <p>Om kunderna använder referensimplementeringen måste de dessutom se till att det inte finns några typoser i filen <span class="codeph"> flashaccess-refimpl.properties</span> där det primära och ytterligare certifikatet har angetts. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError  </span> </td> 
   <td colname="col3"> <p>Den programspecifika underfelkoden är inte känd för Flash Access. <span class="codeph"> subErrorId </span> innehåller ett serverspecifikt fel från utgivarens anpassade licensserver. Servern returnerade ett fel i det programspecifika namnutrymmet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication  </span> </td> 
   <td colname="col3"> <p>Det här felet inträffar när innehållet har konfigurerats för att be klienterna autentisera innan licenserna hämtas. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">Distributörens programvara ska autentisera användaren och sedan hämta licensen igen. <p>Om tjänsten inte har för avsikt att använda autentisering loggar du identifieringen av det innehåll som orsakar felet. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">Det här felet ska inte kräva eskalering, såvida inte innehållet ska konfigureras för att kräva autentisering. <p>I det här fallet bör du paketera om det felaktiga innehållet med rätt policy. Om innehållet är rätt paketerat finns mer information i Diagnostikpolicy/licensavvikelser. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Körningsfel för licenser som inte täcks ovan</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid  </span> </td> 
   <td colname="col3"> <p>Den köpta licensen är inte giltig än. Kontrollera om klientklockan inte är rätt inställd för att lösa problemet. Om du vill ställa in klientklockan paketerar du om innehållet eller ändrar licensserverkonfigurationen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired  </span> </td> 
   <td colname="col3"> Hämta tillbaka licensen från servern. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired  </span> </td> 
   <td colname="col3"> <p>Du måste meddela användarna att de inte kan spela upp det här innehållet förrän policyn har upphört att gälla. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform  </span> </td> 
   <td colname="col3"> <p>Den här plattformen tillåts inte att spela upp innehållet eftersom innehållsleverantören till exempel har konfigurerat Adobe Access att neka innehåll till Adobe Access på en plattform eller en delad domänbunden licens är bunden till en delad domäntoken som är avsedd för en annan partition. </p> <p>CDM kan orsaka det här felet om innehållet inte paketerades med en lämplig (CDM-funktionsstyrd) paketerarcertifiering. </p> <p>Om innehållet paketeras med ett felaktigt PHDS/PHLS-certifikat kan innehållet fungera i Chrome men inte i andra webbläsare (eller tvärtom). <p>Tips:  Detta beror på att Chrome använder olika PHDS/PHLS-certifikat. </p>Bekräfta vilket certifikat som används genom att dumpa informationen i innehållets metadata och leta efter <i>mottagarcertifikaten</i>. Mer information finns i <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion  </span> </td> 
   <td colname="col3"> Uppgradera till den senaste versionen av TVSDK för Android. <p>Lös problemet genom att utföra någon av följande åtgärder: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Uppgradera AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">För Flash Player uppgraderar du AdobeCP-modulen och försöker spela upp igen. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform  </span> </td> 
   <td colname="col3"> <p>Den här plattformen tillåts inte att spela upp innehållet eftersom innehållsleverantören till exempel har konfigurerat Access för att neka innehåll till FP/AIR på en plattform. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion  </span> </td> 
   <td colname="col3"> Uppgradera till den senaste versionen av TVSDK för Android. <p>Detta inträffar om innehållet eller servern är konfigurerad att neka uppspelning till en viss version av Flash- eller AIR-körtiderna. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">Om användaren befinner sig i ett operativsystem där Flash kan uppgraderas bör distributörens programvara uppmana användaren att uppgradera Flash och försöka igen. Annars rekommenderar du användaren att använda en annan dator. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">Om fel 3337s misstänks, identifiera om det förekommer för visst innehåll och paketera om innehållet. Om innehållet har paketerats på rätt sätt kan du läsa Diagnostikpolicy/licensavvikelser </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType  </span> </td> 
   <td colname="col3"> <p>Det går inte att identifiera anslutningstypen och principen kräver att du aktiverar utdataskydd. Problemet förväntas bara om innehållet paketeras för att kräva digitalt eller analogt utdataskydd. </p> <p>Ett problem i versioner av Flash Player som är äldre än version 11.8.800.168 orsakade att fel 3338 ibland inträffade i innehåll som enligt profilen är <span class="codeph"> USE IF AVAILABLE</span>. Problemet har åtgärdats i version 11.8.800.168 och senare. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">Distributörens programvara väljer en variant av innehållet som inte kräver utdataskydd (till exempel en SD-variant av en HD-ström). <p>Om fel 3338 uppstår i <span class="codeph"> USE_IF_AVAILABLE </span>-innehåll kontrollerar du om det finns ett versionsnummer för spelaren. Om spelarversionen är mindre än 11.8.800.168 rekommenderar du att du uppgraderar Flash Player. Om fel 3338 inträffar i versioner över 11.8.800.168 loggar du vilket innehåll som orsakade felet. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">Distributören bör kontrollera vilket innehåll som orsakar det här felet och verifiera att innehållets princip är inställd <span class="codeph"> NO_PROTECTION</span> eller <span class="codeph"> USE_IF_AVAILABLE</span> för analoga och digitala utdata. <p>Om innehållet av misstag paketeras med <span class="codeph"> NO_OUTPUT</span> eller <span class="codeph"> OBLIGATORISKT</span> paketerar du om innehållet. Om innehållet är rätt paketerat kan du läsa Diagnostikpolicy/licensavvikelser. I annat fall eskalera till Adobe. </p> </li> 
    </ul> <p>Mer information finns i <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> Getting unknown 3338 errors when your DRM policy is set to USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed  </span> </td> 
   <td colname="col3"> Det går inte att spela upp på den analoga enheten. Lös problemet genom att ansluta en digital enhet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail  </span> </td> 
   <td colname="col3"> Det går inte att spela upp innehåll eftersom den anslutna analoga externa visningsenheten (skärm/TV) inte har rätt funktioner (enheten har till exempel inte Macrovision eller ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed  </span> </td> 
   <td colname="col3"> Det går inte att spela upp innehåll på en digital enhet. <p>Viktigt:  Problemet bör inte uppstå i en produktionsmiljö eftersom utgivare inte ska tillåta digital uppspelning. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail  </span> </td> 
   <td colname="col3"> Den anslutna digitala externa visningsenheten (skärm/TV) har inte rätt funktioner. Enheten har till exempel inte HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed  </span> </td> 
   <td colname="col3"> <p>Gäller inte för Android. </p> <p>Det här felet inträffar för närvarande när en ny version av Flash släpps upp. Det beror på att Flash uppgraderades medan Flash var öppet, vilket försätter Flash i ett felaktigt tillstånd tills webbläsaren startas om. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">Distributörens programvara ska utföra följande uppgifter: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Rekommendera att användaren stänger eller avslutar alla webbläsare och sedan öppnar igen. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Kontrollera om Flash har aktuell version. <p>Om versionen inte är aktuell kan du råda kunden att uppgradera, stänga alla flikar i webbläsaren och öppna den igen. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">Om ett fel uppstår efter att webbläsaren har startats om kan du eskalera till Adobe. <p>När en ny version släpps rekommenderar vi att du kontaktar Adobe Support för att se om problemet med bakgrundsuppdateringar har åtgärdats. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModul  </span> </td> 
   <td colname="col3"> Gäller inte för Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError  </span> </td> 
   <td colname="col3"> <p>Gäller inte för Android. </p> <p>Det här felet inträffar när en del av Flash eller AIR inte installerades korrekt. </p> <p>Distributörens programvara ska göra något av följande: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Be användaren avinstallera och installera om AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">För Flash Player, ring <span class="codeph"> System.update</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed  </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">Distributörens programvara ska göra något av följande: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">Om AIR är det bara att anropa <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">Om Flash inte kan användas på grund av felen 3322 eller 3346 bör användare gå till <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> och följa instruktionerna i Adobe-artikeln för att återställa DRM-licensarkivet programmatiskt. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">Om det här felet inträffar ofta bör distributören ange information om frekvensspelarversionen och webbläsarversionen för Adobe. </li> 
    </ul> <p>Mer information finns i följande forumartiklar: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM-fel 3322/3346/3368 i Chrome (Info-Bar-problem)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 3322- eller 3346-fel efter maskinvaruändring</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InsufficientDeviceCapabilities  </span> </td> 
   <td colname="col3"> <p>Den primära innebörden av det här felet är att licensen har en begränsning som klientens DRM-certifikat anger att den inte kan uppfylla. Följande maskinvarufunktioner definieras när klientens DRM-certifikat utfärdas: 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Icke-användartillgänglig buss</b>. Om <b>true</b> flödar det dekrypterade mediet aldrig över en buss eller in i huvudminnet, där ett program kan komma åt det. <p>Om <b>false</b> kanske innehållet är tillgängligt för programmet efter dekryptering. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Maskinvarans pålitlighetsrot</b>. Om <b>true</b> verifierades all programvara som läses in vid starten på enheten mot en nyckel eller sammanfattning som bara är tillgänglig i maskinvaran. <p>Båda dessa begränsningar kontrolleras på klientsidan när licensen öppnas mot DRM-certifikatet för klienten och felet är omedelbart. Dessa begränsningar kan även kontrolleras på serversidan innan licensen utfärdas. </p> </li> 
     </ul> </p> <p>Den andra innebörden av det här felet är att licensen har principen "Jailbreak Enforcement" och en jailbreak har upptäckts på enheten. Den här kontrollen görs regelbundet på klientsidan och kan inte kontrolleras på serversidan. </p> <p>Distributörerna kan uppdatera reglerna och ta bort begränsningarna. Om du har profiler för enhetsfunktioner skickar du kommandot för principuppdatering till flaggan <span class="codeph"> -devCapabilitiesV1</span> utan argument. Ange <span class="codeph"> policy.enforcementJailbreak=false</span> för tvångsupphävning. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired  </span> </td> 
   <td colname="col3"> Hårt stoppintervall har gått ut. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh  </span> </td> 
   <td colname="col3"> Servern körs i en version som är högre än den högsta version som stöds av klienten. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow  </span> </td> 
   <td colname="col3"> Servern körs i en version som är lägre än den lägsta version som stöds av klienten. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid  </span> </td> 
   <td colname="col3"> Domäntoken var ogiltig. Åtgärda problemet genom att registrera dig hos domänen igen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld  </span> </td> 
   <td colname="col3"> Domäntoken är äldre än den token som krävs för licensen. Du löser problemet genom att registrera dig hos domänen igen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew  </span> </td> 
   <td colname="col3"> Domäntoken är nyare än den token som krävs för licensen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired  </span> </td> 
   <td colname="col3"> Domäntoken har gått ut. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed  </span> </td> 
   <td colname="col3"> Domänanslutningen misslyckades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCorcorrespondingRoot  </span> </td> 
   <td colname="col3"> Det gick inte att hitta någon rotlicens för en V3-lövlicens. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense  </span> </td> 
   <td colname="col3"> Ingen giltig inbäddad licens hittades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail  </span> </td> 
   <td colname="col3"> Det går inte att spela upp eftersom den anslutna analoga enheten inte har ett AVS-skydd. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail  </span> </td> 
   <td colname="col3"> Det går inte att spela upp eftersom den anslutna analoga enheten inte har CGMS-A-skydd. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired  </span> </td> 
   <td colname="col3"> Innehåll kräver domänregistrering. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain  </span> </td> 
   <td colname="col3"> Datorn är inte registrerad i domänen för de angivna metadata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError  </span> </td> 
   <td colname="col3"> Den asynkrona åtgärden tog längre tid än <span class="codeph"> maxOperationTimeout</span>. Endast returnerat av iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError  </span> </td> 
   <td colname="col3"> Den skickade M3U8-spellistan hade innehåll som inte stöds. Endast returnerat av iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId  </span> </td> 
   <td colname="col3"> <p>Ramverket begärde enhets-ID, men det returnerade värdet var tomt. </p> <p>Användaren bör inte markera kryssrutan <span class="uicontrol"> Tillåt identifierare för skyddat innehåll</span> i Chrome-inställningarna. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed  </span> </td> 
   <td colname="col3"> <p>Den här kombinationen av webbläsare och plattform tillåter inte DRM-skyddad uppspelning i Incognito-läge. </p> <p>Distributörens programvara bör råda användaren att avsluta Incognito-läget eller använda en annan webbläsare. Mer information finns i <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM-fel 3365 orsak och upplösning</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter  </span> </td> 
   <td colname="col3"> <p>Värdmiljön anropade Access-biblioteket med en felaktig parameter. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature  </span> </td> 
   <td colname="col3"> signeringen av m3u8-manifestet misslyckades. Returneras endast av iOS DRMNative Framework eller AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>Användaren avbröt åtgärden eller har angett inställningar som inte tillåter åtkomst till systemet. </p> <p>Det här felet uppstår bara när SWF-versionen är 19 eller senare. För bakåtkompatibilitet genereras 3321 när SWF-filen är version 18 eller tidigare. </p> <p>Distributörens programvara bör vägleda användaren till en förklaring av hur den tillåter åtkomst till plugin-program som inte är i begränsat läge. Mer information finns i <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Google Chrome's unsandbox access deny</a> and <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM Error 3322/3346/3368 in Chrome (Info-Bar Problems)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>Ett nödvändigt webbläsargränssnitt är inte tillgängligt. Problemet inträffar bara på Pepper. Det kan finnas en felmatchning mellan plugin-programmet för Flash och webbläsarversionen. </p> <p>Distributörens programvara bör hjälpa användaren att se till att den senaste versionen av webbläsaren är installerad. </p> <p> Om det här felet ökar och motsvarar en webbläsaruppdatering som släpps, eskalerar du till Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>Användaren har inaktiverat inställningen <span class="uicontrol"> Tillåt identifierare för skyddat innehåll</span>. </p> <p>Tips:  Det här felet uppstod med Pepper-versionerna 13.0.0.x eller senare. </p> <p>Distributörens programvara bör vägleda användaren att aktivera inställningen <span class="uicontrol"> Tillåt identifierare för skyddat innehåll</span>. </p> <p>Distributörens åtgärdsteam bör vägleda användaren att aktivera inställningen <span class="uicontrol"> Tillåt identifierare för skyddat innehåll</span>. </p> <p>Mer information finns i <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_</span><span class="codeph"> NoOPConstraintInPixelConstraints</span> </td> 
   <td colname="col3"> <p>Felaktig upplösning baserad på begränsningar för utdataskydd i licensen. </p> <p>Distributörens programvara ska visa ett felmeddelande. Be användaren rapportera problemet till distributören med en innehållstitel. </p> <p>Distributören bör paketera om innehållet med en giltig profil. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>Innehållets upplösning är större än den maximala upplösning som anges i utdataskyddsbegränsningen. </p> <p>Om distributörens åtgärdsteam ser det här felet i sina loggar bör de granska den upplösningsbaserade utdataskyddsprofilen och vid behov paketera om innehållet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstam</span> </td> 
   <td colname="col3"> <p>Innehållets upplösning är större än upplösningen som anges av den aktuella utdataskyddsbegränsningen. </p> <p>Om distributörens åtgärdsteam ser det här felet i sina loggar bör de granska den upplösningsbaserade utdataskyddsprofilen och vid behov paketera om innehållet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Misslyckades under kommunikationsbearbetning på klientsidan, till exempel generering av begäranden, svarsbearbetning, felaktig autentiseringstoken och så vidare. </p> <p>Om distributörens åtgärdsteam ser det här felet i sina loggar bör de granska den upplösningsbaserade utdataskyddsprofilen och vid behov paketera om innehållet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Värden för videouppspelning {#section_7079501250C2487499639F92EC774525}

Gränssnittet Video Encoder i AVE returnerar dessa videouppspelningsmeddelanden i metadataobjektet `NATIVE_ERROR`.

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Värde för metadatanyckeln NATIVE_ERROR_CODE </th> 
   <th colname="col2" class="entry"> Värde för metadatanyckeln NATIVE_ERROR_NAME </th> 
   <th colname="col3" class="entry"> Beskrivning </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> Periodens slut. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> LYCKADES</span> </td> 
   <td colname="col3"> Åtgärden lyckades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Asynkron åtgärd. Åtgärden har begärts. Information om lyckade/misslyckade åtgärder kommer att vara tillgänglig senare. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Åtgärden är inte möjlig på grund av ett filslutsvillkor (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> Avkodaren misslyckades vid körning. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Det gick inte att öppna maskinvaruavkodaren. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND  </span> </td> 
   <td colname="col3"> Resursen kan inte hittas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR  </span> </td> 
   <td colname="col3"> Allmänt fel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR  </span> </td> 
   <td colname="col3"> Ett feltillstånd som videomotorn inte kan återställas från. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE  </span> </td> 
   <td colname="col3"> Nätverksfel, försöker återställa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE  </span> </td> 
   <td colname="col3"> Resursens storlek kan inte bestämmas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED  </span> </td> 
   <td colname="col3"> Funktionen är inte implementerad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> OUT_OF_MEMORY  </span> </td> 
   <td colname="col3"> Slut på minne. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR  </span> </td> 
   <td colname="col3"> Ett fel uppstod när mediefilen parsades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN  </span> </td> 
   <td colname="col3"> Resursen har en storlek, men är okänd. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW  </span> </td> 
   <td colname="col3"> Underflödesvillkor. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG  </span> </td> 
   <td colname="col3"> Konfigurationen stöds inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION  </span> </td> 
   <td colname="col3"> Åtgärden stöds inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT  </span> </td> 
   <td colname="col3"> Har inte initierats än. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER  </span> </td> 
   <td colname="col3"> Ogiltig parameter. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Åtgärden tillåts inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> Åtgärden tillåts endast när den pausas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> Åtgärden kan inte användas på filer med enbart ljud. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> Tidigare sökåtgärd pågår fortfarande. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED  </span> </td> 
   <td colname="col3"> Resursen har inte angetts. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> Det angivna värdet ligger utanför intervallet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Ogiltig söktid. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> Den angivna filen överensstämmer inte med den förväntade syntaxen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> Det gick inte att skapa en nödvändig komponent. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Det gick inte att skapa DRM-kontext. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> Behållartypen stöds inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Sökningen misslyckades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Kodeken stöds inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> Nätverket är inte tillgängligt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Det gick inte att hämta data från nätverket. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> ÖVERFLÖDE</span> </td> 
   <td colname="col3"> Spill. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Videoprofilen stöds inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> Ett försök att utföra en åtgärd gjordes på en HOLD-period eller en period som ännu inte har lästs in. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> Den angivna tidslängden för ersättning är ogiltig eller sträcker sig utanför strömmens slut. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> API kan inte anropas från fel tråd. För det mesta för API-element som endast ska anropas från huvudtråden. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Fragmentläsningsfel. Det finns ingen redundans. Motorn kommer att försöka läsa nästa fragment. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> AVBRUTEN</span> </td> 
   <td colname="col3"> Åtgärden avbröts av ett explicit anrop om att avbryta eller förstöra. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Det går inte att spela upp den här versionen av HLS-media. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Det går inte att redundansväxla. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> Tidsgränsen för HTTP-hämtning har uppnåtts. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN  </span> </td> 
   <td colname="col3"> Användarens nätverksanslutning är inte tillgänglig. Uppspelningen kan avbrytas när som helst och återupptas när anslutningen är tillgänglig. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Ingen användbar bithastighetsprofil hittades i strömmen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> Manifestet har en felaktig signatur. Det misslyckades med signeringstestet av manifestet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> Det går inte att läsa in en spelningslista. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> Det gick inte att ersätta den som angetts i ett Infoga-API. Det innebär att infogningen lyckades, men inte ersättningen. Ersättningen kan misslyckas om manifestet som ska ersättas har tagits bort från tidslinjen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM växlar till en asymmetrisk profil. Alla profiler förväntas vara justerade i längd. Annars kommer den här varningen att kastas och uppspelningen kan innehålla hopp. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> Live-fönstret förväntas bara flyttas framåt. Om inte kommer den här varningen att kastas och fönstret kommer inte att läsas. Därför kan det finnas hopp (eller stopp/lång paus) i uppspelningen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> Live-fönstret har flyttats utanför den aktuella perioden. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> Den innehållslängd som rapporterades av HTTP-servern matchade inte den faktiska mediestorleken. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> Medieläsaren kan inte läsa vidare eftersom den har nått den tid som anges av setHoldAt API. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD  </span> </td> 
   <td colname="col3">Medieläsaren kan inte läsa in segment eftersom den har nått slutet av det aktiva fönstret. Inläsning av segment återupptas när servern annonserar nya media till det aktiva fönstret. Det här läget nås vanligtvis om: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">Bufferttiden <span class="codeph"> för </span> är för hög (lika med eller högre än varaktigheten för live-fönstret). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">En kombination av ett eller flera API:er för att infoga/radera har ersatt fler media än de lade till. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">Nästa period är en aktiv period med en väntande medieersättning (på grund av InsertBy API-anrop) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING  </span> </td> 
   <td colname="col3"> Ljud- och videointerfolieringen i mediet är inte korrekt gjord. Detta är ett paketeringsfel. Varningen skickas när skillnaden överstiger två sekunder. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHZED</span> </td> 
   <td colname="col3"> HLS-uppspelning har inte aktiverats i Flash Player. Se AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> Avkodaren tog emot ett felaktigt prov som inte kan avkodas. Det här är vanligtvis inget allvarligt fel, men det indikerar att det kan finnas fel i ljud/video. För många instanser av det här felet indikerar felaktig kodning eller felaktig fil. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> När uppspelningen har startat får inte intervallet Infoga/Ersätt innehålla läshuvudet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> Infogningar efter rullning är inte tillåtna på direktmedia. De tillåts dock efter att servern har markerat mediet som fullständigt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Ett mycket sällsynt problem som aldrig skulle inträffa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> Strömmen följer inte paketeringsrekommendationen att alltid placera H264 SPS/PPS i en AVCC. Problem med sökning/uppspelning kan eventuellt visas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> Ersättningen som anges i ett Infoga API har bara delvis utförts. Detta inträffar när replaceDuration sträcker sig över tidslinjens varaktighet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> Det uppstod ett fel när återgivningsspellistan lästes in. Detta gäller endast AVE, inte FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> Åtgärden gör ingenting. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> Segmentet kan inte spelas upp och hoppas över vid fel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Inkompatibelt renderingsläge. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED  </span> </td> 
   <td colname="col3"> Webbprotokollet som används i URL:en stöds inte. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Fel vid parsning av mediefil. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> Manifestfilen ändrades på ett oväntat sätt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Det går inte att utföra en delad åtgärd på en tidslinje. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Det går inte att utföra en raderingsåtgärd på en tidslinje. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Hämtade inte nästa fragment. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Det finns ingen tidslinje i en intern datastruktur. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> Ingen avlyssnare hittades i en intern datastruktur. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Det gick inte att starta ljudet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> Det finns ingen ljudmottagare i en intern datastruktur. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Det gick inte att öppna filen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Det går inte att skriva till en fil. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Det går inte att läsa från en fil. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Det uppstod ett fel vid analys av ID3-data. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR  </span> </td> 
   <td colname="col3"> Det gick inte att läsa in innehållet på grund av säkerhetsbegränsningar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> Tidslinjens varaktighet är för kort. Om det här är en direktström kan det hända att buffring sker ofta. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> Strömmen har växlats till en ström med enbart ljud. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> Strömmen har växlats från enbart ljud till en ström med video. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND  </span> </td> 
   <td colname="col3"> Det går inte att hitta nyckeln. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> Nyckeln är ogiltig. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> Nyckelservern returnerar ingen nyckel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Det går inte att hantera uppdateringen av huvudmanifestet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Orapporterad tid (PTS) - avbrott hittades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Omatchat ljud- och videoavbrott hittades. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Det uppstod ett fel när media spelades upp i <i>tricks play</i>-läge. Trick-uppspelningsläget avslutas och flödet pausas. Anropa <span class="codeph"> Play()</span> för att spela upp media i normalläge. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> Spelaren är utanför det aktiva fönstret och måste söka framåt för att komma ifatt. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Kryptovärden {#section_39365E545CAC49B9A4D4678657BB2155}

Krypteringsmodulen för videomotorn i Adobe returnerar dessa meddelanden i metadataobjektet `NATIVE_ERROR`.

| Värde för metadatanyckeln NATIVE_ERROR_CODE | Värde för metadatanyckeln NATIVE_ERROR_NAME | Betydelse |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | Algoritmen som används stöds inte. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | Data är skadade. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Bufferten är för liten. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Felaktigt certifikat. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Sammandragsuppdatering. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Sammanfattning. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Felaktig parameter. |
