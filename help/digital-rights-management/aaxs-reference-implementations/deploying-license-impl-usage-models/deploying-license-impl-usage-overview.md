---
seo-title: Implementera översikten över användningsmodeller
title: Implementera översikten över användningsmodeller
uuid: 1041bb84-9996-4284-b2a0-d6fc6d4b73d9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Implementera översikten över användningsmodeller {#implementing-the-usage-models-overview}

Referensimplementeringen innehåller affärslogik som visar hur du aktiverar följande fyra olika användningsmodeller för ett paketerat innehåll:

* Ladda ned till eget (DTO)
* Uthyrning/video-on-demand (VOD)
* Prenumeration (all-du-can-eat)
* Reklamfinansierad

Om du vill aktivera demonstrationen av användningsmodellen anger du den anpassade egenskapen `RI_UsageModelDemo=true` vid paketering. Om du paketerar innehåll med kommandoradsverktyget för Media Packager anger du:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om du inte aktiverar det valfria demoläget vid paketeringen använder licensservern den policy som angavs vid paketeringen för att utfärda en licens. Om flera profiler har angetts använder licensservern den första giltiga principen.

I filmen styr serverns affärslogik de faktiska attributen för de genererade licenserna. Vid paketeringen får innehållet endast innehålla minimal policyinformation. Principen behöver bara ange om autentisering krävs för att få tillgång till innehållet. Om du vill aktivera alla fyra användningsmodellerna inkluderar du en policy som tillåter anonym åtkomst (för den annonsfinansierade modellen) och en princip som kräver autentisering av användarnamn/lösenord (för de övriga tre användningsmodellerna). När ett klientprogram begär en licens kan det avgöra om användaren ska tillfrågas om autentisering baserat på autentiseringsinformationen i profilerna.

För att styra den användningsmodell som en viss användare ska få en licens enligt kan poster läggas till i databasen för referensimplementering. Tabellen `Customer` innehåller användarnamn och lösenord för autentisering av användare. Det anger också om användaren har en prenumeration. Användare med prenumerationer får licenser enligt *prenumerationsmodellen* . Om du vill ge en användare åtkomst under *Hämta till egen* eller *Video på begäran* kan en post läggas till i `CustomerAuthorization` tabellen, som anger varje del av innehållet som användaren har åtkomst till och användningsmodellen. Mer information om hur du fyller i varje tabell finns i [!DNL PopulateSampleDB.sql] skriptet.

När en användare begär en licens kontrollerar Reference Implementation-servern de metadata som klienten skickade för att avgöra om innehållet paketerades med `RI_UsageModelDemo` egenskapen. I så fall används följande affärsregler:

* Om någon av profilerna kräver autentisering:

   * Om begäran innehåller en giltig autentiseringstoken söker du efter användaren i kunddatabastabellen. Om användaren hittades:

      * Om `Customer.IsSubscriber` egenskapen är `true`genererar du en licens för *prenumerationsanvändningsmodellen* och skickar den till användaren.

      * Leta efter en post i databastabellen för den här användaren och innehålls-ID:t `CustomerAuthorization` . Om en post hittades:

         * Om `CustomerAuthorization.UsageType` så är `DTO`fallet genererar du en licens för *Ladda ned till egen* modell och skickar den till användaren.

         * Om `CustomerAuthorization.UsageType` så är `VOD`fallet genererar du en licens för *Video On Demand* -användningsmodellen och skickar den till användaren.
   * Om ingen av profilerna tillåter anonym åtkomst:

      * Om det inte finns någon giltig autentiseringstoken i begäran returnerar du felet &quot;autentisering krävs&quot;.
      * Annars returneras ett &quot;ej auktoriserat&quot; fel.


* Om någon av profilerna tillåter anonym åtkomst skapar du en licens för den annonsfinansierade användningsmodellen och skickar den till användaren.

Innan referensimplementeringsservern kan utfärda licenser för demonstrationen av användningsmodellen måste servern konfigureras för att ange hur licenser ska genereras för var och en av de fyra användningsmodellerna. Detta görs genom att ange en profil för varje användningsmodell. Referensimplementeringen innehåller fyra exempelprinciper ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) eller så kan du byta ut dina egna policyer. I [!DNL flashaccess-refimpl.properties]anger du följande egenskaper för att ange vilken profil som ska användas för varje användningsmodell och placerar principfilerna i den katalog som anges av `config.resourcesDirectory` egenskapen:

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```

