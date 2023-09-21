---
title: Implementera översikten över användningsmodeller
description: Implementera översikten över användningsmodeller
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Implementera översikten över användningsmodeller {#implementing-the-usage-models-overview}

Referensimplementeringen innehåller affärslogik som visar hur du aktiverar följande fyra olika användningsmodeller för ett paketerat innehåll:

* Ladda ned till eget (DTO)
* Uthyrning/video-on-demand (VOD)
* Prenumeration (all-du-can-eat)
* Reklamfinansierad

Om du vill aktivera demonstrationen av användningsmodellen anger du den anpassade egenskapen `RI_UsageModelDemo=true` vid paketeringstid. Om du paketerar innehåll med kommandoradsverktyget för Media Packager anger du:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Om du inte aktiverar det valfria demoläget vid paketeringen använder licensservern den policy som angavs vid paketeringen för att utfärda en licens. Om flera profiler har angetts använder licensservern den första giltiga principen.

I filmen styr serverns affärslogik de faktiska attributen för de genererade licenserna. Vid paketeringen får innehållet endast innehålla minimal policyinformation. Principen behöver bara ange om autentisering krävs för att få tillgång till innehållet. Om du vill aktivera alla fyra användningsmodellerna inkluderar du en policy som tillåter anonym åtkomst (för den annonsfinansierade modellen) och en princip som kräver autentisering av användarnamn/lösenord (för de övriga tre användningsmodellerna). När ett klientprogram begär en licens kan det avgöra om användaren ska tillfrågas om autentisering baserat på autentiseringsinformationen i profilerna.

För att styra den användningsmodell som en viss användare ska få en licens enligt kan poster läggas till i databasen för referensimplementering. The `Customer` tabellen innehåller användarnamn och lösenord för autentisering av användare. Det anger också om användaren har en prenumeration. Användare med prenumerationer får licenser under *Prenumeration* användningsmodell. Ge en användare åtkomst under *Ladda ned till Own* eller *Video on Demand* användningsmodeller kan en post läggas till i `CustomerAuthorization` tabell, som anger varje del av innehållet som användaren har åtkomst till och användningsmodellen. Se [!DNL PopulateSampleDB.sql] skript för information om hur varje tabell fylls i.

När en användare begär en licens kontrollerar Reference Implementation-servern de metadata som klienten skickade för att avgöra om innehållet paketerades med `RI_UsageModelDemo` -egenskap. I så fall används följande affärsregler:

* Om någon av profilerna kräver autentisering:

   * Om begäran innehåller en giltig autentiseringstoken söker du efter användaren i kunddatabastabellen. Om användaren hittades:

      * Om `Customer.IsSubscriber` egenskapen är `true`, generera en licens för *Prenumeration* användningsmodell och skicka den till användaren.

      * Leta efter en post i `CustomerAuthorization` databastabell för den här användaren och innehålls-ID:t. Om en post hittades:

         * If `CustomerAuthorization.UsageType` är `DTO`, generera en licens för *Hämta till egen* användningsmodell och skicka den till användaren.

         * If `CustomerAuthorization.UsageType` är `VOD`, generera en licens för *Video On Demand* användningsmodell och skicka den till användaren.

   * Om ingen av profilerna tillåter anonym åtkomst:

      * Om det inte finns någon giltig autentiseringstoken i begäran returnerar du felet &quot;autentisering krävs&quot;.
      * Annars returneras ett &quot;ej auktoriserat&quot; fel.

* Om någon av profilerna tillåter anonym åtkomst skapar du en licens för den annonsfinansierade användningsmodellen och skickar den till användaren.

Innan referensimplementeringsservern kan utfärda licenser för demonstrationen av användningsmodellen måste servern konfigureras för att ange hur licenser ska genereras för var och en av de fyra användningsmodellerna. Detta görs genom att ange en profil för varje användningsmodell. Referensimplementeringen innehåller fyra exempelprinciper ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) eller du kan ersätta din egen policy. I [!DNL flashaccess-refimpl.properties]anger du följande egenskaper för att ange vilken profil som ska användas för varje användningsmodell och placerar principfilerna i den katalog som anges av `config.resourcesDirectory` egenskap:

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
