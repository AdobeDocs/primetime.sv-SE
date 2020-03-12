---
description: Loggfilerna som genereras av Adobe Primetime DRM Server för Skyddad strömning finns i den katalog som anges av LicenseServer.LogRoot.
seo-description: Loggfilerna som genereras av Adobe Primetime DRM Server för Skyddad strömning finns i den katalog som anges av LicenseServer.LogRoot.
seo-title: Loggfiler
title: Loggfiler
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Loggfiler{#log-files}

Loggfilerna som genereras av Adobe Primetime DRM Server för Skyddad strömning finns i den katalog som anges av LicenseServer.LogRoot.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om de aktuella loggfilerna tas bort eller flyttas medan servern körs, kanske loggfilen inte skapas på nytt. Därför kan viss logginformation tas bort.

## Loggkatalogstruktur {#section_F490A483D60145ADBC21038914C39203}

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

## Global loggfil {#section_1CFA90748142439C9F3BE380969539DA}

Den globala loggfilen [!DNL flashaccess-global.log]finns i *LicenseServer.LogRoot*. Loggen kan innehålla loggmeddelanden som Adobe Primetime DRM Java SDK eller loggmeddelanden kan ha genererats när servern har initierats.

## Partitionsloggfil {#section_5660137CD6AA40519E72A4315534846B}

Partitionsloggfilen, [!DNL flashaccess-partition.log], finns i [!DNL <LicenseServer.LogRoot>/flashaccesserver] katalogen. Den innehåller loggmeddelanden som har genererats under bearbetning av en licensbegäran.

## Klientloggfil {#section_F0257CC0831647F18A746B4F02E3E910}

Varje klientorganisations loggfil, [!DNL flashaccess-tenant.log], finns i [!DNL &lt;LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>]. Klientloggen innehåller granskningsinformation som beskriver varje licens som skapas för den här klienten.
