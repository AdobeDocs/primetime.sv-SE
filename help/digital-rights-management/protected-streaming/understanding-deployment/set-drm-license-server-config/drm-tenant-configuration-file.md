---
description: Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.
title: Konfigurationsfil för innehavare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Konfigurationsfil för klientorganisation{#tenant-configuration-file}

Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.

Varje klientorganisation stöder sin egen instans av den här konfigurationsfilen som finns i `<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`. I katalogen `configs/flashaccessserver/tenants/sampletenant` finns ett exempel på en klientkonfigurationsfil.

Du kan ange alla filsökvägar i klientkonfigurationsfilen som absoluta sökvägar eller som sökvägar som är relativa till klientens konfigurationskatalog (`<LicenseServer.ConfigRoot>/flashaccessserver/tenants/<tenantname>`).

Klientkonfigurationsfilen innehåller:

* *Transportautentiseringsuppgifter*  - Anger en eller flera transportreferenser (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en [!DNL .pfx]-fil och ett lösenord, eller ett alias för en autentiseringsuppgift som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

   Mer information om när ytterligare autentiseringsuppgifter krävs finns i *Hantera certifikatuppdateringar* i *Använda Adobe Primetime DRM SDK för att skydda innehåll*.

* *Autentiseringsuppgifter*  för licensserver - Anger en eller flera autentiseringsuppgifter för licensservern (certifikat och privat nyckel) som Adobe har utfärdat. Du kan ange autentiseringsuppgifter för licensservern som en sökväg till en [!DNL .pfx]-fil och ett lösenord, eller ett alias för en autentiseringsuppgift som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

   Mer information om när ytterligare autentiseringsuppgifter krävs finns i *Hantera certifikatuppdateringar* i *Använda Adobe Primetime DRM SDK för att skydda innehåll*.

* *Certifikat*  för nyckelserver - Anger eventuellt det certifikat för licensserver som Adobe har utfärdat. Du kan ange nyckelserverns licensservercertifikat som en sökväg till en [!DNL .cer]-fil eller ett alias för ett certifikat som lagras på en HSM. Det här alternativet måste anges för att utfärda licenser för innehåll som paketeras med en DRM-princip som kräver fjärrnyckelleverans för iOS-enheter.

* *Anpassade författare*  - Ange anpassade behörighetsklasser som ska anropas för varje licensbegäran om det behövs. Om flera auktoriserare anges anropas de i den ordning som anges.
* *Lista över auktoriserade paket*  - Anger valfritt certifikat som identifierar enheter som är auktoriserade att paketera innehåll för den här licensservern. Om inget paketerarcertifikat anges utfärdar servern licenser för innehåll som paketeras av en paketerare. Om servern tar emot en licensbegäran från en obehörig paketerare, nekas begäran.
* *Minimiversion som stöds för* klienterSe Använda Adobe Primetime DRM SDK för att skydda innehåll.

* *Användningsregler*

   * *License Caching*  - Anger hur länge du kan lagra licensen på klienten. Som standard är cachning av licenser inaktiverat. Om du vill aktivera licenscache-lagring under en begränsad tidsperiod måste du ange slutdatum eller antal sekunder som licensen ska lagras för (med början när licensen utfärdas). Om du anger antalet sekunder till 0 inaktiveras licenscachelagring.

      >[!NOTE]
      >
      >Alla licenser som servern för skyddad direktuppspelning har utfärdat inkluderar en förfalloperiod på 24 timmar (8 6400 sekunder). Det här värdet gäller implicit som en övre gräns för vilket slutdatum eller vilken varaktighet som helst som är inställt för licenscachelagring, med ett maximalt värde på 86400 sekunder, även om schemat framtvingar högre gränser.

   * *Spela upp höger*  - Du måste ange minst en rättighet. Om du anger flera behörigheter använder klienten den första rättigheten som uppfyller alla krav.

      * *Utdataskydd*  - Anger om utdata till externa återgivningsenheter ska skyddas.
      * *AIR- och SWF-programbegränsningar*  - valfria tillåtelselista i SWF- och AIR-program som kan spela upp innehållet (till exempel tillåts bara de angivna programmen). SWF-program identifieras av en URL eller av sammandraget i SWF-filen och den längsta tid som går åt för hämtning och verifiering av sammandraget.

         Mer information om hur du beräknar SWF-sammanfattningen finns i *Hash-beräkningen för SWF.*

         Ett utgivar-ID och valfritt program-ID, lägsta version och högsta version identifierar AIR- och iOS-program. Om du inte anger några programbegränsningar kan innehållet spelas upp i alla SWF- och AIR-program.

      * *DRM- och körningsmodulbegränsningar*  - Anger den lägsta säkerhetsnivå som krävs för DRM/körningsmodulen. Du kan även inkludera en blockeringslista med versioner som inte får spela upp innehållet. Modulversioner identifieras av attribut, till exempel operativsystem och/eller ett versionsnummer.

         DRM-modulbegränsningar och begränsningar för körningsmodulen har nu stöd för följande ytterligare attribut:

         * `oemVendor`
         * `model`
         * `screenType`

         Följande attribut är nu valfria:

         * `osVersion`
         * `version`
      * *Krav*  för enhetskapacitet - Anger om maskinvarufunktioner som krävs för att få åtkomst till innehåll ska användas.
      * *Krav*  för identifiering av Jailbreak - Anger eventuellt att uppspelning inte tillåts för enheter där jailbreak upptäcks.



Mer information finns i kommentarerna i exempelfilen för klientkonfiguration.
