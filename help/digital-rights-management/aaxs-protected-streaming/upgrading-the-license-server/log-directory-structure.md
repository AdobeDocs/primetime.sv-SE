---
title: Loggkatalogstruktur
description: Loggkatalogstruktur
copied-description: true
exl-id: 8c52fd85-cc46-41da-b5a1-41b5d61da6ad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '16'
ht-degree: 0%

---

# Loggkatalogstruktur{#log-directory-structure}

Loggkatalogen har följande struktur:

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
