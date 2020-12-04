---
seo-title: Konfigurationsfil för innehavare
title: Konfigurationsfil för innehavare
uuid: 6e5c82c9-b8f5-4fca-8325-a884b2c779f7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Konfigurationsfil för klientorganisation {#tenant-configuration-file}

Konfigurationsfilen flashaccess-tenant.xml innehåller inställningar som gäller för en specifik klientorganisation för licensservern. Varje klientorganisation har en egen instans av den här konfigurationsfilen som finns i *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname*. I katalogen [!DNL configs/flashaccessserver/tenants/sampletenant] finns ett exempel på en klientkonfigurationsfil.

Du kan ange alla filsökvägar i klientkonfigurationsfilen som absoluta sökvägar eller sökvägar i förhållande till klientens konfigurationskatalog (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*klientnamn*).

Klientkonfigurationsfilen innehåller:

* **Transportautentiseringsuppgifter**  - Anger en eller flera transportreferenser (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en pfx-fil och ett lösenord, eller ett alias för en referens som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och. Se &quot;[Hantera certifikatuppdateringar](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)&quot; i *Använda Adobe Access SDK för att skydda innehåll* för mer information om när ytterligare autentiseringsuppgifter krävs.
* **Autentiseringsuppgifter**  för licensserver - Anger en eller flera autentiseringsuppgifter för licensservern (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en pfx-fil och ett lösenord, eller ett alias för en referens som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och. Mer information om när ytterligare autentiseringsuppgifter behövs finns i Hantera certifikatuppdateringar i *Använda Adobe Access SDK för att skydda innehåll *.
* **Nyckelservercertifikat**  - valfritt. Anger nyckelserverns licensservercertifikat som utfärdas av Adobe. Kan anges som en sökväg till en .cer-fil eller ett alias till ett certifikat som lagras på en HSM. Det här alternativet måste anges för att licenser ska kunna utfärdas för innehåll som paketerats med en profil som kräver fjärrnyckelleverans för iOS-enheter.
* **Anpassade författare**  - valfritt. Anger anpassade behörighetsklasser som ska anropas för varje licensbegäran. Om flera auktoriserare anges anropas de i den ordning som anges. Mer information finns i &quot;[Anpassade auktoriseringstillägg](../../aaxs-protected-streaming/custom-authorization-extensions.md)&quot;.
* **Lista över auktoriserade paket**  - valfritt. Anger certifikat som identifierar entiteter som är auktoriserade att paketera innehåll för den här licensservern. Om inget paketerarcertifikat har angetts utfärdar servern licenser för innehåll som paketerats av en paketerare.
* **Minimiversion**  av klient som stöds (se  *Använda Adobe Access SDK för att skydda innehåll*).
* **Användningsregler**

   * **Licenscache**  - valfritt. Anger hur länge licensen kan lagras på klienten. Som standard är cachning av licenser inaktiverat. Om du vill aktivera cache-lagring av licenser under en begränsad tidsperiod anger du slutdatumet eller antalet sekunder som licensen ska lagras för (med början när licensen utfärdas). Om du anger antalet sekunder till 0 inaktiveras licenscachelagring.

      Observera att alla licenser som utfärdas av servern för skyddad direktuppspelning har en förfalloperiod på 24 timmar (8 6400 sekunder). Det här värdet gäller därför implicit som en övre gräns till vilket slutdatum eller vilken varaktighet som helst som är inställt för licenscachning, med ett maximalt värde på 86400 sekunder, även om schemat har högre gränser.

   * **Spela upp höger**  - minst en höger måste anges. Om flera rättigheter anges kommer klienten att använda den första rättigheten som den uppfyller alla krav för.

      * **Utdataskydd**  - Anger om utdata till externa återgivningsenheter ska skyddas.
      * **AIR- och SWF-programbegränsningar**  - valfria tillåtelselista i SWF- och AIR-program som kan spela upp innehållet (dvs. endast de angivna programmen tillåts). SWF-program identifieras av en URL eller av sammandraget i SWF-filen och den längsta tid som går åt för hämtning och verifiering av sammandraget. Information om hur du beräknar SWF-sammanfattningen finns i avsnittet &quot;SWF-hash-kalkylator&quot;. AIR- och iOS-program identifieras av ett utgivar-ID och valfritt program-ID, lägsta version och högsta version. Om inga programbegränsningar anges kan innehållet spelas upp av alla SWF- eller AIR-program.
      * **DRM- och körningsmodulbegränsningar**  - Anger den lägsta säkerhetsnivå som krävs för DRM/körningsmodulen. Du kan även inkludera en blockeringslista med versioner som inte får spela upp innehållet. Modulversioner identifieras av attribut som operativsystem och/eller ett versionsnummer. DRM-modulbegränsningar och begränsningar för körningsmodulen har nu stöd för följande ytterligare attribut:

         * `oemVendor`
         * `model`
         * `screenType`

         Följande attribut är nu valfria:

         * `osVersion`
         * `version`
      * **Krav**  för enhetskapacitet - Anger om maskinvarufunktioner som krävs för att få åtkomst till innehåll ska användas.
      * **Krav**  för identifiering av Jailbreak - Anger eventuellt att uppspelning inte tillåts för enheter där jailbreak upptäcks.



Mer information finns i kommentarerna i exempelfilen för klientkonfiguration.
