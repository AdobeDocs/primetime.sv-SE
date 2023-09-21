---
title: Uppdatera en DRM-princip med Java API
description: Uppdatera en DRM-princip med Java API
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Uppdatera en DRM-princip med Java API {#updating-a-drm-policy-with-the-java-api}

Så här uppdaterar du en DRM-princip med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer i projektet som finns i [Konfigurera utvecklingsmiljön](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Skapa en DRM `Policy` och läsa DRM-principen från en fil eller databas.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Uppdatera DRM `Policy` genom att ange dess egenskaper, t.ex. dess namn och användningsregler.

   ```java
   // Change the DRM policy name.  
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

1. Serialisera den uppdaterade DRM-filen `Policy` och lagra det i en fil eller databas.

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

Se `com.adobe.flashaccess.samples.policy.UpdatePolicy` i kommandoradsverktygen för referensimplementering [!DNL samples] -katalog för källan för den här exempelkoden.
