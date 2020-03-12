---
description: Så snart licensservern läser någon av licensserverkonfigurationsfilerna (global eller klientkonfiguration) cachelagras konfigurationsinformationen i minnet. Därför behöver filerna inte läsas från disken för varje licensbegäran. Servern tillåter dock att de flesta värden i konfigurationsfilerna ändras utan att det krävs någon omstart av servern för att ändringarna ska börja gälla.
seo-description: Så snart licensservern läser någon av licensserverkonfigurationsfilerna (global eller klientkonfiguration) cachelagras konfigurationsinformationen i minnet. Därför behöver filerna inte läsas från disken för varje licensbegäran. Servern tillåter dock att de flesta värden i konfigurationsfilerna ändras utan att det krävs någon omstart av servern för att ändringarna ska börja gälla.
seo-title: Konfigurationsfiler uppdateras
title: Konfigurationsfiler uppdateras
uuid: 34b3247c-3458-49de-b1b0-dc0ebbf61c88
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Konfigurationsfiler uppdateras{#updating-configuration-files}

Så snart licensservern läser någon av licensserverkonfigurationsfilerna (global eller klientkonfiguration) cachelagras konfigurationsinformationen i minnet. Därför behöver filerna inte läsas från disken för varje licensbegäran. Servern tillåter dock att de flesta värden i konfigurationsfilerna ändras utan att det krävs någon omstart av servern för att ändringarna ska börja gälla.

När du ändrar konfigurationsfilen lagrar licensservern den tid som filen senast ändrades. Vid ett konfigurerbart intervall kontrollerar servern om filändringstiden har ändrats. Om den har ändrats läser servern automatiskt in innehållet i konfigurationsfilen igen.

Om du vill styra hur ofta servern söker efter uppdateringar måste du ange attributet `refreshDelaySeconds` i `Caching` elementet i den globala konfigurationsfilen. Om `refreshDelaySeconds` till exempel är inställt på 3 600 sekunder kommer servern att uppdatera konfigurationen inom högst en timme från ändringstiden för konfigurationsfilen. Om värdet `refreshDelaySeconds` är 0 söker servern efter konfigurationsuppdateringar vid varje begäran. Vi rekommenderar inte att du anger `refreshDelaySeconds` ett lågt värde i någon produktionsmiljö eftersom detta kan påverka prestandan.

Elementet styr också `Caching` hur många klientkonfigurationer som cachelagras samtidigt. Du kan ange det här värdet till ett tal som är mindre än det totala antalet klientorganisationer för att begränsa mängden minne som används för att cachelagra konfigurationsinformationen. Om en begäran tas emot för en klientorganisation som inte finns i cachen, läses konfigurationen in innan begäran kan behandlas. Om cacheminnet är fullt tas den senast använda klientorganisationen bort från cacheminnet.

Den cachelagrade versionen av konfigurationen fortsätter att användas i följande situationer (fram till nästa gång servern söker efter uppdateringar):

* Om en ändring sparas i en konfigurationsfil eller i någon av de certifikatfiler som refereras i [!DNL flashaccess-tenant.xml] filen medan servern försöker läsa filen
* Om filens tidsstämpel visar sig vara mindre än en sekund före den aktuella tiden
* Om filens tidsstämpel är i framtiden

Om det inte finns någon cachelagrad version misslyckas inläsningen av konfigurationen och ett fel returneras till klienten. Servern försöker sedan att läsa in filen igen nästa gång den tar emot en begäran för den klienten.

## Uppdaterar den globala konfigurationsfilen {#section_AA546C72442646CFB8906AEEBDF50587}

Du kan när som [!DNL flashaccess-global.xml] helst ändra HSM-lösenordet i. Ändringarna börjar gälla nästa gång servern läser in konfigurationsfilen igen. Ändringar av elementen Loggning och Caching läses dock inte in igen. Du måste starta om servern innan ändringarna för dessa element börjar gälla.

## Uppdaterar klientkonfigurationsfilen {#section_71624DB8DF28480F84F34F0FF7FD4365}

Du kan när som helst ändra alla värden som anges i [!DNL flashaccess-tenant.xml] filen. Ändringarna börjar gälla nästa gång servern läser in konfigurationsfilen igen. Servern söker även efter ändringar i alla autentiseringsfiler ( [!DNL .pfx]) och i paketerarens whitelist-certifikatfiler som refereras i klientkonfigurationsfilen.
