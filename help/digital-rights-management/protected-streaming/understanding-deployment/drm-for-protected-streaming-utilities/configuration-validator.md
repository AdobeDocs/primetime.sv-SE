---
description: Adobe rekommenderar att du kör verktyget Configuration Validator innan du startar servern om du gör ändringar i konfigurationsfilen. Detta verktyg kan upptäcka de flesta konfigurationsfel tidigt, innan de orsakar fel under bearbetningen av begäran.
title: Konfigurationsvaliderare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Konfigurationsvaliderare{#configuration-validator}

Adobe rekommenderar att du kör verktyget Configuration Validator innan du startar servern om du gör ändringar i konfigurationsfilen. Detta verktyg kan upptäcka de flesta konfigurationsfel tidigt, innan de orsakar fel under bearbetningen av begäran.

Om du vill köra valideraren skriver du:

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

eller

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

För var och en av licensserverkonfigurationsfilerna kan valideraren utföra filbaserad validering, vilket säkerställer att XML-filen är välformaterad och följer konfigurationsfilens schema.

Om du vill utföra filbaserad validering på den globala konfigurationsfilen skriver du:

```
Validator --<file path>/flashaccess-global.xml --global
```

Om du vill utföra filbaserad validering av klientkonfigurationsfilen skriver du:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

Valideraren kan även utföra distributionsbaserad validering. Förutom att kontrollera överensstämmelse med schemat verifierar den här valideringsnivån även att de angivna värdena är giltiga. Det ser till exempel till att refererade filer finns.

Distributionsbaserad validering kan utföras på följande nivåer:

* `Tenant` — Validerar konfigurationsfilen och autentiseringsuppgifterna för en viss klientorganisation. Om du vill validera konfigurationen för `<tenant1>` skriver du:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — Validerar den globala konfigurationsfilen och klientverifieringen för alla klientorganisationer. Om du vill utföra global distributionsbaserad validering skriver du:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

