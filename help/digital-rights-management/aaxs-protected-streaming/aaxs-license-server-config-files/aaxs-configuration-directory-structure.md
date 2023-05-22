---
description: Adobe Access Server för skyddad strömning kräver två typer av konfigurationsfiler, en global konfigurationsfil (flashaccess-global.xml) och en klientkonfigurationsfil för varje klientorganisation (flashaccess-tenant.xml).
title: Struktur för konfigurationskatalog
exl-id: 6561c001-798c-4503-8afb-93580d957372
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Konfigurationsfiler för licensserver och Konfiguration av katalogstruktur {#configuration-directory-structure}

Adobe Access Server för skyddad strömning kräver två typer av konfigurationsfiler: en global konfigurationsfil (flashaccess-global.xml) och en klientkonfigurationsfil för varje klientorganisation (flashaccess-tenant.xml).

När du har redigerat konfigurationsfilerna rekommenderar Adobe att du använder verktygen i Adobe Access Server för skyddad direktuppspelning för att verifiera att filerna är välformade. Mer information finns i &quot;[Konfigurationsvaliderare](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

För att undvika att göra lösenord tillgängliga i klartext i konfigurationsfilerna måste alla lösenord som anges i den globala konfigurationsfilen och klientkonfigurationsfilen krypteras. Mer information om kryptering av lösenord finns i &quot;[Lösenordsfasare](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

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
