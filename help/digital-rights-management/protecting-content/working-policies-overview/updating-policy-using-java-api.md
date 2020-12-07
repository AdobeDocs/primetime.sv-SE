---
seo-title: Uppdatera en DRM-princip med Java API
title: Uppdatera en DRM-princip med Java API
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Uppdatera en DRM-princip med Java API {#updating-a-drm-policy-with-the-java-api}

Så här uppdaterar du en DRM-princip med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som anges i [Konfigurera utvecklingsmiljön](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) i projektet.
1. Skapa en DRM `Policy`-instans och läs DRM-principen från en fil eller databas.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Uppdatera DRM `Policy`-objektet genom att ange dess egenskaper, till exempel dess namn och användningsregler.

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

1. Serialisera det uppdaterade DRM `Policy`-objektet och lagra det i en fil eller databas.

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

I katalogen `com.adobe.flashaccess.samples.policy.UpdatePolicy` i Command Line Tools [!DNL samples] för Reference Implementation finns information om källan för den här exempelkoden.
