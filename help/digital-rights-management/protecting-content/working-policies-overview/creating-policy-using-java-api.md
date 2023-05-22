---
title: Skapa en DRM-princip med Java API
description: Skapa en DRM-princip med Java API
copied-description: true
exl-id: fcae76c3-4e51-449d-b6d5-2138bf1c583e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Skapa en DRM-princip med Java API {#creating-a-drm-policy-with-the-java-api}

Så här skapar du en DRM-princip med Java API:

1. Konfigurera utvecklingsmiljön och inkludera alla JAR-filer i projektet som finns i [Konfigurera utvecklingsmiljön.](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Skapa en `com.adobe.flashaccess.sdk.policy.Policy` -objektet och ange dess egenskaper, inklusive rättigheter, varaktighet för licenscache och slutdatum för DRM-princip.

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

1. Serialisera DRM `Policy` och lagra det i en fil eller databas.

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

Se [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] i kommandoradsverktygen för referensimplementering [!DNL samples] katalog för den fullständiga källan för exempelkoden.
