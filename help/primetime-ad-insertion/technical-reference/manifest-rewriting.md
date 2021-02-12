---
title: Regler för omskrivning av manifest och annonshämtning
description: 'Regler för omskrivning av manifest och annonshämtning '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Regler för omskrivning av manifest och annonshämtning {#manifest-rewriting}

Primetime Ad Insertion kan skriva om fragment och hämta resurser med hjälp av enkla sök- och ersättningsregler.  Detta kan användas för att nedkonvertera https till http-begäranden, vilket skulle öka prestandan genom att ta bort TLS-handskakningar.  Detta kan också användas för att leverera annonsresurser och CDN-resurser från samma CDN.

Regler definieras som sökningar/ersättningar för reguljära uttryck och kan användas för att omforma URL:er innan de skickas samt efter att de har infogats i ett manifest.

Den här exempelregeln konverterar alla annonsbegäranden till domain.com från https till http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

Följande regel kommer att använda innehållets-CDN för att leverera annonser som finns i CDN för Adobe-lagring.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

Regler kan namnges och aktiveras/inaktiveras genom att ändra parametern `ptprotoswitch` i Bootstrap-API:t, som är en kommaseparerad lista över regler som ska köras.  Dessa två regler kan till exempel båda köras genom att ställa in `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

Kontakta din tekniska support för att skapa/aktivera dessa regler för ditt konto.