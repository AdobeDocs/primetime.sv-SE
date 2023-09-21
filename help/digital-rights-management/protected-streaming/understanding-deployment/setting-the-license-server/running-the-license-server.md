---
title: Köra DRM-servern för skyddad strömning
description: Köra DRM-servern för skyddad strömning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Köra DRM-servern för skyddad strömning {#running-the-drm-server-for-protected-streaming}

Innan du kan starta Adobe Primetime DRM Server for Protected Streaming rekommenderar vi att du kontrollerar att inställningarna i konfigurationsfilerna är giltiga.

Du kan kontrollera att inställningarna är giltiga med hjälp av de verktyg som finns på licensservern. (Se *Konfigurationsvaliderare* i den här guiden.

Om du vill starta Tomcat och licensservern måste du köra [!DNL catalina.bat start] eller [!DNL catalina.sh start] från Tomcat&#39;s [!DNL bin] katalog.

När servern har startats måste du verifiera att den har konfigurerats korrekt genom att öppna `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` i ett webbläsarfönster. Om klientkonfigurationen har lästs in visas ett bekräftelsemeddelande.

## Loggfiler {#log-files}

Loggfilerna som genereras av Adobe Primetime DRM Server för Skyddad strömning finns i den katalog som anges av LicenseServer.LogRoot.

>[!NOTE]
>
>Om de aktuella loggfilerna tas bort eller flyttas medan servern körs, kanske loggfilen inte skapas på nytt. Därför kan viss logginformation tas bort.

### Loggkatalogstruktur {#section_F490A483D60145ADBC21038914C39203}

Loggkataloger är strukturerade för att vara lätta att använda. Loggkatalogen har följande struktur:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

### Global loggfil {#section_1CFA90748142439C9F3BE380969539DA}

Den globala loggfilen, [!DNL flashaccess-global.log]finns i *LicenseServer.LogRoot*. Loggen kan innehålla loggmeddelanden om att Adobe Primetime DRM Java SDK eller loggmeddelanden kan ha genererats under den tid som servern har initierats.

### Partitionsloggfil {#section_5660137CD6AA40519E72A4315534846B}

Partitionsloggfilen, [!DNL flashaccess-partition.log]finns i `<LicenseServer.LogRoot>/flashaccesserver` katalog. Den innehåller loggmeddelanden som har genererats under bearbetning av en licensbegäran.

### Klientloggfil {#section_F0257CC0831647F18A746B4F02E3E910}

Varje klientorganisations loggfil, [!DNL flashaccess-tenant.log]finns i `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. Klientloggen innehåller granskningsinformation som beskriver varje licens som genereras för den här klienten.

## Konfigurationsfiler uppdateras {#updating-configuration-files}

Så snart licensservern läser någon av licensserverkonfigurationsfilerna (global eller klientkonfiguration) cachelagras konfigurationsinformationen i minnet. Därför behöver filerna inte läsas från disken för varje licensbegäran. Servern tillåter dock att de flesta värden i konfigurationsfilerna ändras utan att det krävs någon omstart av servern för att ändringarna ska börja gälla.

När du ändrar konfigurationsfilen lagrar licensservern den tid som filen senast ändrades. Vid ett konfigurerbart intervall kontrollerar servern om filändringstiden har ändrats. Om den har ändrats läser servern automatiskt in innehållet i konfigurationsfilen igen.

Om du vill styra hur ofta servern söker efter uppdateringar måste du ange `refreshDelaySeconds` i `Caching` -element i den globala konfigurationsfilen. Om `refreshDelaySeconds` är inställt på 3 600 sekunder kommer servern att uppdatera konfigurationen inom högst en timme från ändringsdatumet för konfigurationsfilen. If `refreshDelaySeconds` anges till 0, söker servern efter konfigurationsuppdateringar vid varje begäran. Vi rekommenderar inte att du anger `refreshDelaySeconds` till ett lågt värde i alla produktionsmiljöer eftersom detta kan påverka prestandan.

The `Caching` -elementet styr också hur många klientkonfigurationer som cachelagras samtidigt. Du kan ange det här värdet till ett tal som är mindre än det totala antalet klientorganisationer för att begränsa mängden minne som används för att cachelagra konfigurationsinformationen. Om en begäran tas emot för en klientorganisation som inte finns i cachen, läses konfigurationen in innan begäran kan behandlas. Om cachen är full tas den senast använda klientorganisationen bort från cachen.

Den cachelagrade versionen av konfigurationen fortsätter att användas i följande situationer (fram till nästa gång servern söker efter uppdateringar):

* Om en ändring sparas i en konfigurationsfil eller i någon av de certifikatfiler som refereras i [!DNL flashaccess-tenant.xml] när servern försöker läsa filen
* Om filens tidsstämpel visar sig vara mindre än en sekund före den aktuella tiden
* Om filens tidsstämpel är i framtiden

Om det inte finns någon cachelagrad version misslyckas inläsningen av konfigurationen och ett fel returneras till klienten. Servern försöker sedan att läsa in filen igen nästa gång den tar emot en begäran för den klienten.

### Uppdaterar den globala konfigurationsfilen {#section_AA546C72442646CFB8906AEEBDF50587}

Du kan ändra HSM-lösenordet i [!DNL flashaccess-global.xml] när som helst. Ändringarna börjar gälla nästa gång servern läser in konfigurationsfilen igen. Ändringar av elementen Loggning och Caching läses dock inte in igen. Du måste starta om servern innan ändringarna för dessa element börjar gälla.

### Uppdaterar klientkonfigurationsfilen {#section_71624DB8DF28480F84F34F0FF7FD4365}

Du kan ändra alla värden som anges i [!DNL flashaccess-tenant.xml] när som helst. Ändringarna börjar gälla nästa gång servern läser in konfigurationsfilen igen. Servern söker även efter ändringar i alla autentiseringsuppgifter ( [!DNL .pfx]) filer och tillåtelselista-certifikatfiler för paketerare som refereras i klientkonfigurationsfilen.
