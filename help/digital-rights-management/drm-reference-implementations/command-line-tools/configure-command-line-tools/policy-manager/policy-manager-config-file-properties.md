---
description: 'null'
keywords: hard stop
seo-description: 'null'
seo-title: Konfigurationsegenskaper
title: Konfigurationsegenskaper
uuid: 216921d1-a9c1-4650-9dce-c025836986e5
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# Konfigurationsegenskaper {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>För egenskapsnamn som innehåller `.n``n` representerar heltalet ett heltal som börjar med 1 och ökar för varje instans av egenskapen. Exempel: `policy.license.customProp.n`.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Alternativ för egenskap/kommandorad </th> 
   <th colname="2" class="- topic/entry entry"> Beskrivning </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">principnamn</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Namnet på DRM-principen som kan läsas av människor. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">boolesk</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Följande villkor gäller: 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">Om true krävs en HTTPS Key Server för nyckelleverans till iOS. </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">Om inget anges är standardvärdet false. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforcementJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforcementJailbreak</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Om värdet är true tillåts inte uppspelning när jailbreak upptäcks på enheter som stöder jailbreak-identifiering. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -kritisk</span> <i class="+ topic/ph hi-d/i ">boolesk</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Ställer in kritiken för DRM-principen: 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">Om true måste servern förstå alla delar av DRM-principen, som representerar standardbeteendet. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">Om false kan servern ignorera DRM-principattribut som den inte känner igen. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Licensservercertifikat vars offentliga nyckel används för att kryptera rotkrypteringsnyckeln för den <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> förbättrade licenskedjan</a>. This property specifies a file that only includes the certificate. <p>Obs!  Både PEM- och DER-format stöds. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Anger rotkrypteringsnyckeln för den <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> förbättrade licenskopplingen</a>. Om ingen nyckel har angetts och Förbättrad licenskoppling är aktiverad, genereras en slumpmässig nyckel automatiskt. </p> <p>Nyckeln måste vara 16 byte lång och anges som hexadecimala värden. Blanksteg mellan hexvärdena är valfritt. För uppdateringar är kommandoradsalternativet inte tillgängligt och egenskapen ignoreras. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Om domänregistrering krävs anger <i>url</i> URL:en för en domänserver. För uppdateringar är kommandoradsalternativet inte tillgängligt och egenskapen ignoreras. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">Anger om anonym domänregistrering tillåts. Anger egenskapen till true eller innehåller det här kommandoradsalternativet för att tillåta anonym åtkomst. <p>Obs! Det här alternativet kan inte användas med <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namnutrymme</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Autentiseringsnamnområdet för domänregistrering. Om det anges måste klienten autentisera med ett användarnamn och lösenord som utfärdades av den angivna utfärdaren. </p> <p>För uppdateringar är kommandoradsalternativet inte tillgängligt och egenskapen ignoreras. </p> <p>Obs! Det här alternativet kan inte användas med <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Begränsningar för analogt utdataskydd och följande värden stöds: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> OBLIGATORISKT</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>DRM-klienter som är begränsade från åtkomst till skyddat innehåll. Det här alternativet anger en lista med versioner av DRM-moduler som inte får användas (blockeringslista). </p> <p>Värdet består av kommaseparerade <span class="codeph"> name=value</span> -par i följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Ytterligare namn/värde-par måste vara kommaavgränsade. Till exempel <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklsit</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Programmiljöer är begränsade från åtkomst till skyddat innehåll. Det här alternativet anger en lista med versioner av runtime-moduler som inte får användas (blockeringslista). </p> <p>Värdet består av kommaseparerade <span class="codeph"> name=value</span> -par i följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|program|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Ytterligare namn/värde-par måste vara kommaavgränsade. Till exempel <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger de enhetsfunktioner som krävs för att få åtkomst till skyddat innehåll. Värdet består av kommaseparerade <span class="codeph"> name=value</span> -par i följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Till exempel <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. </p> <p>Under en uppdatering måste du använda <span class="codeph"> -devCapabilitiesV1</span> utan de återstående argumenten som tar bort begränsningen för enhetsfunktioner. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger hur ofta klienter måste skicka synkroniseringsmeddelanden till servern. </p> <p>Om egenskapen inte är inställd skickar klienterna inte synkroniseringsmeddelanden när de spelar upp innehåll som är skyddat med en DRM-princip. Värdet består av kommaseparerade <span class="codeph"> name=value</span> -par i följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">Följande lista innehåller ytterligare information om alternativen: 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(obligatoriskt) <span class="codeph"> start</span> anger att klienten måste starta synkroniseringen med servern under de angivna minuterna sedan den senaste synkroniseringen. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(valfritt) <span class="codeph"> force</span> är sannolikheten (0-100) med vilken klienten måste framtvinga ett synkroniseringsmeddelande under uppspelning. </li> 
     </ul>Under uppdateringen använder du <span class="codeph"> -sync</span> utan de återstående argumenten för att ta bort synkroniseringskraven. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Anger om den här DRM-principen har en rotlicens. <p>Mer information finns i <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Förbättrad licenskanning</a>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">Det datum efter vilket innehållet börjar gälla. Du kan använda något av följande format: 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> <p>Exempel: <span class="codeph"> 2009-01-31</span> betyder 31 januari klockan 12:00. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sek</span> <p>Exempel: <span class="codeph"> 2009-01-31-14:30:00</span> betyder 31 januari klockan 2:30. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Datumet innan innehållet blir ogiltigt. </p> <p>Obs! Du kan inte ange <span class="codeph"> policy.expiration.endDate</span> och <span class="codeph"> policy.expiration.duration</span> samtidigt. </p> <p>Exempel: 2009-01-31-14:30:00 betyder att innehållet upphör att gälla den 31 januari klockan 2:30. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tiden i minuter när innehållet blir ogiltigt. Tiden börjar när du paketerar innehåll. </p> <p>Obs! Du kan inte ange <span class="codeph"> policy.expiration.endDate</span> och <span class="codeph"> policy.expiration.duration</span> samtidigt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tiden i minuter när en licens kan cachas på klienten. Du kan ställa in den här egenskapen på 0 om du vill förhindra licenscachelagring. Värdet måste vara 0 eller högre. </p> <p>Obs! Du kan inte ange <span class="codeph"> policy.licenseCaching.duration</span> och <span class="codeph"> policy.licenseCaching.endDate</span> samtidigt. </p> <p class="- topic/p ">Den här DRM-principinställningen används bara för licenscachningen på disken och styr inte längden på den cachelagrade licensen i minnet. Licensen kan cachas i minnet även om du inte anger en DRM-princip med en varaktighet på noll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Det datum efter vilket du inte längre kan cachelagra licenser. </p> <p>Obs! Du kan inte ange <span class="codeph"> policy.licenseCaching.duration</span> och <span class="codeph"> policy.licenseCaching.endDate</span> samtidigt. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger om anonym licensköp tillåts. Standardvärdet är <span class="codeph"> false</span>, vilket innebär att användarnamn och lösenord krävs. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Om ett användarnamn och lösenord krävs anger den här egenskapen en valfri namnkvalificerare för användarnamn. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anpassade namn/värde-par som ska användas av servern vid licensköp. Du kan använda följande format för att ange egenskaper: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger uppspelningsfönstret i minuter. Detta värde anger hur länge licensen är giltig efter första gången det skyddade innehållet spelas upp. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Begränsningar för utdataskydd, som måste vara något av följande värden: 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> OBLIGATORISKT</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">Anger vilka OTA-anslutningstyper (over the air) som ska vara tillåtna. Giltiga anslutningstyper är: 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> FLYGPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> Anger den konfigurationsfil i vilken upplösningsbaserade begränsningar definieras. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anger den lägsta säkerhetsnivån som gör att DRM-modulen kan komma åt skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Programkörningsmodulen måste ha minst den angivna lägsta säkerhetsnivån för att kunna komma åt skyddat innehåll. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En tillåtelselista av program som inte är Flash (Adobe AIR, iOS, Android osv.) som kan spela upp skyddat innehåll. Egenskapen måste ha följande format: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">En tillåtelselista med SWF-program som kan spela upp skyddat innehåll. Egenskapen måste ha följande format: </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> är den SWF-fil som används för att beräkna hash-värdet, och <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> är den maximala tiden i sekunder som tillåts för hämtning och verifiering av SWF-filen för slutförande. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Anpassade namn/värde-par som du måste inkludera i licenser när licenserna utfärdas till användare. Du måste ange följande format: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">Du kan definiera det här alternativet flera gånger för flera anpassade egenskaper. </p> </td> 
  </tr> 
 </tbody> 
</table>
