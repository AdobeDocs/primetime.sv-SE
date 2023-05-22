---
title: Uppdaterar översikt över konfigurationsfiler
description: Uppdaterar översikt över konfigurationsfiler
copied-description: true
exl-id: 51c8a0af-9445-4c9e-93bc-af0af0096705
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Uppdaterar översikt över konfigurationsfiler {#updating-configuration-files-overview}

När licensservern har läst någon av licensserverkonfigurationsfilerna (global konfiguration eller klientkonfiguration) cachelagras konfigurationsinformationen i minnet. Därför behöver filerna inte läsas från disken för varje licensbegäran. Servern tillåter dock att de flesta värden i konfigurationsfilerna ändras utan att det krävs någon omstart av servern för att ändringarna ska börja gälla. (Se nedan för mer information om vilka konfigurationsvärden som söks efter uppdateringar.)

För att kunna läsa in konfigurationen igen när ändringar görs lagrar licensservern den tid då filen senast ändrades. Vid ett konfigurerbart intervall kontrollerar servern om ändringstiden för filen har ändrats och läser i så fall in filens innehåll igen.

Om du vill styra hur ofta servern söker efter uppdateringar ställer du in `refreshDelaySeconds` -attributet i Caching-elementet i den globala konfigurationsfilen. Om `refreshDelaySeconds` är inställt på 3 600 sekunder. Det tar högst en timme från det att filen uppdateras för att konfigurationsuppdateringar ska kunna identifieras av servern. If `refreshDelaySeconds` anges till 0, söker servern efter konfigurationsuppdateringar för varje begäran. Inställning `refreshDelaySeconds` till ett lågt värde rekommenderas inte för produktionsmiljöer eftersom det kan påverka prestandan.

Caching-elementet styr också hur många klientkonfigurationer som cachelagras samtidigt. Du kan ange det här värdet till ett tal som är mindre än det totala antalet klientorganisationer för att begränsa mängden minne som används för att cachelagra konfigurationsinformationen. Om en begäran tas emot för en klientorganisation som inte finns i cachen, läses konfigurationen in innan begäran kan behandlas. Om cacheminnet är fullt tas den senast använda klientorganisationen bort från cacheminnet.

Om en ändring sparas i en konfigurationsfil eller i någon av de certifikatfiler som refereras i [!DNL flashaccess-tenant.xml] när servern försöker läsa filen, eller om filens tidsstämpel visar sig vara mindre än en sekund före den aktuella tiden eller i framtiden, används den cachelagrade versionen av konfigurationen tills nästa gång servern söker efter uppdateringar. Om det inte finns någon cachelagrad version misslyckas inläsningen av konfigurationen och ett fel returneras till klienten. Servern försöker att läsa in filen igen nästa gång den tar emot en begäran för den klienten.
