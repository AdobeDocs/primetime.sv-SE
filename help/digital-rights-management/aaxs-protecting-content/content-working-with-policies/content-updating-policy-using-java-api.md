---
title: Uppdatera en princip med Java API
description: Uppdatera en princip med Java API
copied-description: true
exl-id: 1b03f033-0d29-46cc-ae14-d6fef96fe970
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Uppdatera en princip med Java API {#updating-a-policy-using-the-java-api}

Så här uppdaterar du en princip med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som nämns i [Konfigurera utvecklingsmiljön](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) i ditt projekt.
1. Skapa en `Policy` -instans och läsa från en fil eller databas i principen.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Uppdatera `Policy` genom att ange dess egenskaper, till exempel dess namn och användningsregler.

   ```java
     // Change the policy name.  
     policy.setName("UpdatedDemoPolicy");  
   
     // Add DRM module restrictions to the play right  
     for (Right r: policy.getRights()) {  
      if (r instanceof PlayRight) {  
       PlayRight pr = (PlayRight) r;  
       // Disallow Linux versions up to and including 1.9.  Allow  
       // all other OSes and Linux versions above 1.9  
       VersionInfo toExclude = new VersionInfo();  
       toExclude.setOS("Linux");  
       toExclude.setReleaseVersion("1.9");  
       Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
       exclusions.add(toExclude);  
       ModuleRequirements drmRestrictions = new ModuleRequirements();  
       drmRestrictions.setExcludedVersions(exclusions);  
       pr.setDRMModuleRequirements(drmRestrictions);  
       break;  
      }  
     }
   ```

1. Serialisera den uppdaterade `Policy` och lagra det i en fil eller databas.

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

Om du vill se den fullständiga källan för den här exempelkoden går du till `com.adobe.flashaccess.samples.policy.UpdatePolicy` i kommandoradskatalogen för Reference Implementation Tools &quot;samples&quot;.
