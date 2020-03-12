---
seo-title: Skapa en DRM-princip med Java API
title: Skapa en DRM-princip med Java API
uuid: 1672a6d0-e38c-4330-97b0-02147f99db47
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Skapa en DRM-princip med Java API {#creating-a-drm-policy-with-the-java-api}

Så här skapar du en DRM-princip med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer som finns i [Konfigurera utvecklingsmiljön i projektet.](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Skapa ett `com.adobe.flashaccess.sdk.policy.Policy` objekt och ange dess egenskaper, inklusive rättigheter, varaktighet för licenscache och slutdatum för DRM-princip.

   ```java
   // Create a new DRM policy object.  
   // False indicates the DRM policy does not use license chaining.  
   Policy policy = new Policy(false);  
   
   policy.setName("DemoPolicy");  
   
   // Specify that the DRM policy requires authentication to obtain a license.  
   policy.setLicenseServerInfo(new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
   // A DRM policy must have at least one Right, typically the play right  
   PlayRight play = new PlayRight();  
   
   // Users can only view content for 24 hours.  
   play.setPlaybackWindow(24L * 60 * 60);  
   
   // Add the play right to the DRM policy.  
   List<Right> rightsList = new ArrayList<Right>();  
   rightsList.add(play);  
   policy.setRights(rightsList);  
   
   // Licenses can be stored on the client for 7 days after downloading  
   policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
   try {  
       // Content will expire December 31, 2010  
       SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
       policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
   } catch (ParseException e) {  
       // Invalid date specified in dateFormat.parse()  
       e.printStackTrace();  
   } 
   ```

1. Serialisera DRM- `Policy` objektet och lagra det i en fil eller databas.

   ```java
   // Serialize the DRM policy  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("Created DRM policy with ID: " + policy.getId());  
   
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy.pol");  
   out.write(policyBytes);  
   out.close(); 
   ```

Se [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] i [!DNL samples] katalogen Reference Implementation Command Line Tools för den fullständiga källan till exempelkoden.
