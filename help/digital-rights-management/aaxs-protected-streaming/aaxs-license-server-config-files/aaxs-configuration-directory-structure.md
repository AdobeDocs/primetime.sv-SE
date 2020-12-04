---
description: Adobe Access Server för skyddad strömning kräver två typer av konfigurationsfiler, en global konfigurationsfil (flashaccess-global.xml) och en klientkonfigurationsfil för varje klientorganisation (flashaccess-tenant.xml).
seo-description: Adobe Access Server för skyddad strömning kräver två typer av konfigurationsfiler, en global konfigurationsfil (flashaccess-global.xml) och en klientkonfigurationsfil för varje klientorganisation (flashaccess-tenant.xml).
seo-title: Struktur för konfigurationskatalog
title: Struktur för konfigurationskatalog
uuid: c6cfc734-6b7c-4502-9bdb-c7aaca156e0e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Konfigurationsfiler för licensserver och konfigurationskatalogstruktur {#configuration-directory-structure}

Adobe Access Server för skyddad strömning kräver två typer av konfigurationsfiler: en global konfigurationsfil (flashaccess-global.xml) och en klientkonfigurationsfil för varje klientorganisation (flashaccess-tenant.xml).

När du har redigerat konfigurationsfilerna rekommenderar Adobe att du använder verktygen i Adobe Access Server för skyddad direktuppspelning för att verifiera att filerna är välformade. Mer information finns i &quot;[Konfigurationsvaliderare](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

För att undvika att göra lösenord tillgängliga i klartext i konfigurationsfilerna måste alla lösenord som anges i den globala konfigurationsfilen och klientkonfigurationsfilen krypteras. Mer information om kryptering av lösenord finns i &quot;[Lösenordssparare](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

Konfigurationskatalogerna har följande struktur:

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

