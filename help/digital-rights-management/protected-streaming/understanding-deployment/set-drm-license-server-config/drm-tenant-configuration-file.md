---
description: Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.
title: Konfigurationsfil för innehavare
exl-id: 35ec521f-ba17-4a2d-8adb-82b2c6cbe33a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Konfigurationsfil för innehavare{#tenant-configuration-file}

Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.

Varje klientorganisation har stöd för en egen instans av den här konfigurationsfilen som finns i `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. Se `configs/flashaccessserver/tenants/sampletenant` katalog för en exempelklientkonfigurationsfil.

Du kan ange alla filsökvägar i klientkonfigurationsfilen som absoluta sökvägar eller som sökvägar som är relativa till klientens konfigurationskatalog (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

Klientkonfigurationsfilen innehåller:

* *Transportautentiseringsuppgifter* — Anger en eller flera transportreferenser (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en [!DNL .pfx] fil och ett lösenord eller ett alias för en referens som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

   Se *Hantera certifikatuppdateringar* in *Använda Adobe Primetime DRM SDK för att skydda innehåll* om du vill ha mer information om när ytterligare autentiseringsuppgifter krävs.

* *Autentiseringsuppgifter för licensservern* — Anger en eller flera inloggningsuppgifter för licensservern (certifikat och privat nyckel) som Adobe har utfärdat. Du kan ange autentiseringsuppgifter för licensservern som en sökväg till en [!DNL .pfx] fil och ett lösenord eller ett alias för en referens som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

   Se *Hantera certifikatuppdateringar* in *Använda Adobe Primetime DRM SDK för att skydda innehåll* om du vill ha mer information om när ytterligare autentiseringsuppgifter krävs.

* *Certifikat för nyckelserver* — Anger också nyckelserverns licensservercertifikat som Adobe har utfärdat. Du kan ange nyckelserverns licensservercertifikat som en sökväg till en [!DNL .cer] fil eller alias till ett certifikat som lagras på en HSM. Det här alternativet måste anges om du vill utfärda licenser för innehåll som paketeras med en DRM-princip som kräver fjärrnyckelleverans för iOS-enheter.

* *Anpassade författare* — Om du vill kan du ange anpassade behörighetsklasser som ska anropas för varje licensbegäran. Om flera auktoriserare anges anropas de i den ordning som anges.
* *Lista över godkända paket* — Anger eventuellt certifikat som identifierar entiteter som är auktoriserade att paketera innehåll för den här licensservern. Om inget paketerarcertifikat anges utfärdar servern licenser för innehåll som paketeras av en paketerare. Om servern tar emot en licensbegäran från en obehörig paketerare, nekas begäran.
* *Klientversion som stöds minimalt* Se Använda Adobe Primetime DRM SDK för att skydda innehåll.

* *Användningsregler*

   * *Licenscache* — Anger hur länge du kan lagra licensen på klienten. Som standard är cachning av licenser inaktiverat. Om du vill aktivera licenscache-lagring under en begränsad tidsperiod måste du ange slutdatum eller antal sekunder som licensen ska lagras för (med början när licensen utfärdas). Om du anger antalet sekunder till 0 inaktiveras licenscachelagring.

      >[!NOTE]
      >
      >Alla licenser som servern för skyddad direktuppspelning har utfärdat inkluderar en förfalloperiod på 24 timmar (8 6400 sekunder). Det här värdet gäller implicit som en övre gräns för vilket slutdatum eller vilken varaktighet som helst som är inställt för licenscachelagring, med ett maximalt värde på 86400 sekunder, även om schemat framtvingar högre gränser.

   * *Spela upp höger* — Minst en rättighet måste anges. Om du anger flera behörigheter använder klienten den första rättigheten som uppfyller alla krav.

      * *Utdataskydd* — Anger om utdata till externa återgivningsenheter ska skyddas.
      * *AIR och SWF* — Valfritt tillåtelselista i SWF- och AIR-program som kan spela upp innehållet (t.ex. tillåts endast de angivna programmen). SWF-program identifieras av en URL eller av sammanfattningen från SWF och den längsta tiden som krävs för att ladda ned och verifiera sammandraget.

         Se *SWF Hash Calculator* om du vill ha information om hur du beräknar sammandraget i SWF.

         Ett utgivar-ID och valfritt program-ID, lägsta version och högsta version identifierar AIR- och iOS-program. Om du inte anger några programbegränsningar kan innehållet spelas upp i alla SWF- och AIR-program.

      * *Begränsningar för DRM- och körningsmodulen* — Anger den lägsta säkerhetsnivå som krävs för modulen DRM/Runtime. Du kan även inkludera en blockeringslista med versioner som inte får spela upp innehållet. Modulversioner identifieras av attribut, till exempel operativsystem och/eller ett versionsnummer.

         DRM-modulbegränsningar och begränsningar för körningsmodulen har nu stöd för följande ytterligare attribut:

         * `oemVendor`
         * `model`
         * `screenType`

         Följande attribut är nu valfria:

         * `osVersion`
         * `version`
      * *Krav för enhetskapacitet* — Anger vilken maskinvara som krävs för att få åtkomst till innehållet.
      * *Krav för identifiering av Jailbreak* — Alternativt kan du ange att uppspelning inte tillåts för enheter där jailbreak upptäcks.



Mer information finns i kommentarerna i exempelfilen för klientkonfiguration.
