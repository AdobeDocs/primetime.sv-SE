---
description: Du måste konfigurera serveregenskaperna så att de återspeglar din miljö. Du kan göra detta med något av följande
title: Tillämpa egenskaper på servermiljöer
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Tillämpa egenskaper på servermiljöer{#apply-properties-to-server-environments}

Du måste konfigurera serveregenskaperna så att de återspeglar din miljö. Du kan göra detta på något av följande sätt:

* [!DNL flashaccess-i15n.properties] - Prov som ingår i [!DNL .war] filer

* [!DNL AdobeInitial.properties] - Provet finns i [!DNL /shared] på dvd-skivan

   Du kan använda den här filen för att åsidosätta egenskaperna som anges i WAR-filen enligt följande:

   1. Ange åsidosättningsegenskapsvärden i [!DNL AdobeInitial.properties]
   1. Montera [!DNL AdobeInitial.properties] på klassökvägen.

   >[!NOTE]
   >
   >Adobe rekommenderar att du använder [!DNL AdobeInitial.properties] eftersom det gör att du kan uppdatera dina AIR-programfiler utan att riskera att förlora tidigare egenskapskonfigurationsinställningar som du har gjort i [!DNL flashaccess-i15n.properties] -fil.

* Egenskapsmekanismen för Java System.

Du kan använda enskilda egenskaper i dessa specifika servermiljöer:

* *Utveckling*
* *Mellanlagring*
* *Produktion*

Med den här funktionen kan du använda samma WAR-fil för alla servermiljöer. Om du vill använda egenskaper i specifika miljöer lägger du till två understreck (&#39; `__`&#39;) plus en av följande miljökoder till egenskapen *name*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Du kan till exempel ange loggnivån till `INFO` för produktion och staging-servrar, och `DEBUG` för din utvecklingsserver:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

Servern använder den här sökordningen för egenskaper:

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` i Java-systemegenskaper
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` i Java-systemegenskaper

>[!NOTE]
>
>Du måste ange serverns miljönamn som en Java-systemegenskap när du startar servern. Exempel: när du startar Tomcat med [!DNL catalina.bat], ange `CATALINA_OPTS` miljövariabel enligt följande:
>-DENVIRONMENT_NAME=[ DEV | SCEN | PROD ]
