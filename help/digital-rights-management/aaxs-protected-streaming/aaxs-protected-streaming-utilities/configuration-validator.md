---
title: Konfigurationsvaliderare
description: Konfigurationsvaliderare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Konfigurationsvaliderare {#configuration-validator}

Adobe rekommenderar att du kör verktyget Configuration Validator innan du startar servern när ändringar görs i konfigurationsfilen. Detta verktyg kan upptäcka de flesta konfigurationsfel tidigt, innan de orsakar fel under bearbetningen av begäran.

Använd kommandot för att köra valideraren:

```
Validator.bat options  
```

eller kommandot:

```
java -jar libs/flashaccess-validator.jar options 
```

För var och en av licensserverkonfigurationsfilerna kan valideraren utföra filbaserad validering, vilket säkerställer att XML-filen är välformaterad och följer konfigurationsfilens schema. Om du vill utföra filbaserad validering på den globala konfigurationsfilen kör du kommandot:

```
Validator --file path/flashaccess-global.xml --global
```

Kör kommandot om du vill utföra filbaserad validering av klientkonfigurationsfilen:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

Valideraren kan också utföra distributionsbaserad validering. Förutom att kontrollera överensstämmelse med schemat kontrollerar den här valideringsnivån även att de angivna värdena är giltiga (till exempel säkerställer den att det finns refererade filer). Distributionsbaserad validering kan utföras på två nivåer:

* Klient - Verifierar konfigurationsfilen och autentiseringsuppgifter för en specifik klient. Kör kommandot för att validera konfigurationen för &quot;tenant1&quot;:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Global - Verifierar den globala konfigurationsfilen och klientverifieringen för alla klientorganisationer. Kör kommandot för att utföra global distributionsbaserad validering:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
