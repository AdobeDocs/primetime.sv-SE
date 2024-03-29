---
description: Anpassa referensimplementeringen för att integrera Adobe Primetime-autentisering för produktionsmiljön.
title: Integrera Primetime-autentisering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Integrera Primetime-autentisering {#integrate-primetime-authentication}

Anpassa referensimplementeringen för att integrera Adobe Primetime-autentisering för produktionsmiljön.

Integreringen av referensimplementering av Primetime-autentiseringstjänsten fungerar som en demonstration. Om du vill använda integreringen i en produktionsfärdig spelare måste du implementera följande anpassningar:

1. Aktivera eller inaktivera tillståndsflöden.

   The `EntitlementManager` måste först initiera och hämta en instans av Primetime-autentiserings-SDK för att aktiveras. Om `EntitlementManager` initierar inte det här biblioteket, hanteraren inaktiveras.
1. Aktivera `EntitlementManger`från huvudprogramklassen:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Använd `ManagerFactory` för att få en instans av `EntitlementManager`.

   Du måste alltid använda `ManagerFactory` för att hämta en instans av `EntitlementManager`, som `ManagerFactory` underhåller en enda instans av EntitlementManager för programmet. Instansiera aldrig `EntitlementManager` eller `EntitlementManagerOn` klasser genom att använda deras konstruktorer.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   The `ManagerFactory` returnerar en instans av `EntitlementManagerOn`, med aktiverade berättigandeflöden, om du tidigare har anropat `EntitlementManager.initializeAccessEnabler`. Om du inte ringer första gången `EntitlementManager.initializeAccessEnabler`och sedan `ManagerFactory` returnerar en instans av `EntitlementManager`, med berättigandeflödena inaktiverade. 1. Konfigurera begärande-ID.

   Referensimplementeringen är förkonfigurerad med testbegärande-ID inställt på: &quot;REF&quot;. Du kan använda detta begärande-ID för att testa programmet. När du är redo att använda det begärande-ID som du fått från din autentiseringsrepresentant för Primetime, ska du uppdatera programmets [!DNL res/values/strings.xml] med ditt begärande-ID.

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   Dessutom kan du behöva ändra de URL:er som ditt program använder för att ansluta till Primetimes autentiseringstjänster. Dessa inkluderar URL:er för testnings- och produktionsserver för Primetime-autentisering och en URL till en Token Verification Service. Kontakta Adobe Primetime för mer information. 1. Signera begärande-ID:t.

   För att kunna fastställa programmerarens identitet i Primetimes autentiseringssystem skickas programmerarens begärande-ID till autentiseringssystemet Primetime. Som ett extra säkerhetslager måste begärande-ID:t signeras av programmeraren innan det skickas till Adobe. Adobe rekommenderar att Programmeraren installerar en tjänst för att signera begärande-ID på ett betrott nätverk.

   Primetimes referensimplementering visar hur du signerar begärande-ID, men detta är endast till för demonstrationssyften. Adobe rekommenderar starkt att signeringscertifikatet och signaturgeneratorkoden under `com.adobe.primetime.reference.crypto`, ska inte ingå i ett produktionsprogram. I stället bör du flytta den till en betrodd nätverkstjänst.

1. Konfigurera servermiljön.

   Autentiseringstjänsten Primetime kan köras i två olika miljöer:

   * Mellanlagring - Mellanlagringsmiljön används för att testa programmet.
   * Produktion - Produktionsmiljön används för driftsättning av ditt program i realtid.

   Du ställer in URI:er för både staging- och produktionsmiljöer med programmet, men du måste ange vilken av dessa som ska användas av programmet i koden. I `com.adobe.primetime.reference.manager.EntitlementManger` klass, ange `environmentUri` variabel till antingen `STAGING_URI` eller `PRODUCTION_URI` beroende på vilken autentiseringsmiljö du använder.

   >[!NOTE]
   >
   >Angivet begärande-ID (&quot;REF&quot;) bör endast användas med mellanlagringsmiljön.

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. Anpassa MVPD-markeringsstödrastret.

   På urvalssidan för innehållsleverantör visas en tabell med de nio översta PDF-filerna som användaren kan välja bland. Programmet hämtar de nio viktigaste PDF-filerna från en ordnad lista i programmet som matchar de tillgängliga MVPD-filerna som är integrerade med programmeraren i Primetimes autentiseringssystem. Den ordnade listan över de primära PDF-filerna sparas i MVPD-ID:t i autentiseringssystemet Primetime, inte i visningsnamnet för MVPD. Det är viktigt att verifiera att MVPD ID:n i listan över primära MVPD-ID:n matchar MVPD ID:n som är integrerade med programmerarens konto, eftersom ID:n i vissa fall kan vara olika för olika integreringar. Nedan finns den ordnade listan över primära MVPD-filer som finns i klassen `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   Följande tabell innehåller ett exempel på hur den ordnade listan över primära MVPD används. I den första kolumnen visas de MVPD-program som är integrerade med Programmer. Den andra kolumnen är den (förkortade) ordnade listan över MVPD-filer. Den tredje kolumnen är resultatlistan som används för att visa de sex viktigaste PDF-filerna för användaren.

   I det här exemplet används de sex bästa videofilmarna i stället för de nio för att exemplet ska vara enkelt. Lägg märke till hur resultatlistan innehåller skärningspunkten för de två första listorna och har samma ordning som den andra listan. Observera också att AT&amp;T U-verse inte finns med i den slutliga listan eftersom endast de första matchande sex PDF-filerna tas.

| Tillgängliga MVPD-filer | Primära MVPD-filer | Visa 6 MVPD-filer |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Danska</li><li>AT&amp;T U-verterad</li><li>CableOne</li><li>Borghfyr</li><li>Atlantic Broadband</li><li>WOW!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Danska</li><li> TWC</li><li>Cox</li><li>Stadga</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T U-verterad</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Danska</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
