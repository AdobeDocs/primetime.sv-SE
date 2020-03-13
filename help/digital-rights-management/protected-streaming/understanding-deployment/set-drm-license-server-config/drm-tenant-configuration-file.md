---
description: Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.
seo-description: Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.
seo-title: Konfigurationsfil för innehavare
title: Konfigurationsfil för innehavare
uuid: bc9ee4a1-63b6-4362-9929-3e9fe8251075
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Konfigurationsfil för innehavare{#tenant-configuration-file}

Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en viss klientorganisation på licensservern.

Varje klientorganisation har stöd för en egen instans av den här konfigurationsfilen som finns i [!DNL &lt;LicenseServer.ConfigRoot>/flashaccesserver/tenants/<tenantname>]. I katalogen finns ett exempel på en [!DNL configs/flashaccessserver/tenants/sampletenant] klientkonfigurationsfil.

Du kan ange alla filsökvägar i klientkonfigurationsfilen som absoluta sökvägar eller som sökvägar som är relativa till klientens konfigurationskatalog ( [!DNL &lt;LicenseServer.ConfigRoot>/flashaccesserver/tenants/<tenantname>]).

Klientkonfigurationsfilen innehåller:

* *Transportautentiseringsuppgifter* - Anger en eller flera transportreferenser (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en [!DNL .pfx] fil och ett lösenord, eller ett alias för en autentiseringsuppgift som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

   Mer information om när ytterligare autentiseringsuppgifter behövs finns i *Hantera certifikatuppdateringar* i *Använda Adobe Primetimes DRM SDK för att skydda innehåll* .

* *Autentiseringsuppgifter* för licensserver - Anger en eller flera autentiseringsuppgifter för licensservern (certifikat och privat nyckel) som Adobe har utfärdat. Du kan ange autentiseringsuppgifter för licensservern som en sökväg till en [!DNL .pfx] fil och ett lösenord, eller som ett alias för en autentiseringsuppgift som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

   Mer information om när ytterligare autentiseringsuppgifter behövs finns i *Hantera certifikatuppdateringar* i *Använda Adobe Primetimes DRM SDK för att skydda innehåll* .

* *Key Server Certificates* - alternativt anger du Key Server-certifikatet som Adobe har utfärdat. Du kan ange nyckelserverns licensservercertifikat som en sökväg till en [!DNL .cer] fil eller ett alias för ett certifikat som lagras på en HSM. Det här alternativet måste anges för att utfärda licenser för innehåll som paketeras med en DRM-princip som kräver fjärrnyckelleverans för iOS-enheter.

* *Custom Authorizers* - alternativt anger du anpassade behörighetsklasser som ska anropas för varje licensbegäran. Om flera auktoriserare anges anropas de i den ordning som anges.
* *Lista över auktoriserade paket* - Anger valfritt certifikat som identifierar enheter som är auktoriserade att paketera innehåll för den här licensservern. Om inget paketerarcertifikat anges utfärdar servern licenser för innehåll som paketeras av en paketerare. Om servern tar emot en licensbegäran från en obehörig paketerare, nekas begäran.
* *Klientversion* som stöds finns i Använda Adobe Primetime DRM SDK för att skydda innehåll.

* *Användningsregler*

   * *License Caching* - Anger hur länge du kan lagra licensen på klienten. Som standard är cachning av licenser inaktiverat. Om du vill aktivera licenscache-lagring under en begränsad tidsperiod måste du ange slutdatum eller antal sekunder som licensen ska lagras för (med början när licensen utfärdas). Om du anger antalet sekunder till 0 inaktiveras licenscachelagring.

      >[!NOTE]
      >
      >Alla licenser som servern för skyddad direktuppspelning har utfärdat inkluderar en förfalloperiod på 24 timmar (8 6400 sekunder). Det här värdet gäller implicit som en övre gräns för vilket slutdatum eller vilken varaktighet som helst som är inställt för licenscachelagring, med ett maximalt värde på 86400 sekunder, även om schemat framtvingar högre gränser.

   * *Spela upp höger* - Du måste ange minst en rättighet. Om du anger flera behörigheter använder klienten den första rättigheten som uppfyller alla krav.

      * *Utdataskydd* - Anger om utdata till externa återgivningsenheter ska skyddas.
      * *AIR- och SWF-programbegränsningar* - Valfri vitlista över SWF- och AIR-program som kan spela upp innehållet (till exempel tillåts bara de angivna programmen). SWF-program identifieras av en URL eller av sammandraget i SWF-filen och den längsta tid som går åt för hämtning och verifiering av sammandraget.

         Mer information om hur du beräknar SWF-sammanfattningen finns i *SWF-hash-beräkningen* .

         Ett utgivar-ID och valfritt program-ID, lägsta version och högsta version identifierar AIR- och iOS-program. Om du inte anger några programbegränsningar kan innehållet spelas upp i alla SWF- och AIR-program.

      * *DRM- och körningsmodulbegränsningar* - Anger den lägsta säkerhetsnivå som krävs för DRM/körningsmodulen. Du kan även inkludera en svart lista med versioner som inte får spela upp innehållet. Modulversioner identifieras av attribut, till exempel operativsystem och/eller ett versionsnummer.

         DRM-modulbegränsningar och begränsningar för körningsmodulen har nu stöd för följande ytterligare attribut:

         * `oemVendor`
         * `model`
         * `screenType`
         Följande attribut är nu valfria:

         * `osVersion`
         * `version`
      * *Krav på* enhetskapacitet - Anger om maskinvarufunktioner krävs för att få tillgång till innehåll.
      * *Krav* för identifiering av Jailbreak - Alternativt anges att uppspelning inte tillåts för enheter där jailbreak upptäcks.



Mer information finns i kommentarerna i exempelfilen för klientkonfiguration.
