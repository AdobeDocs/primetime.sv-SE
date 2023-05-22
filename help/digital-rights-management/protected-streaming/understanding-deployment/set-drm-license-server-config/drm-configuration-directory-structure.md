---
title: Struktur för konfigurationskatalog
description: Struktur för konfigurationskatalog
copied-description: true
exl-id: e24d3df0-f723-4dad-84d5-984f3350353a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '16'
ht-degree: 0%

---

# Struktur för konfigurationskatalog{#configuration-directory-structure}

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
