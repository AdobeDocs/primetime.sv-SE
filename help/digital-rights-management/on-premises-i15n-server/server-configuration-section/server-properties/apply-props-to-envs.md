---
description: 'Du måste konfigurera serveregenskaperna så att de återspeglar din miljö. Du kan göra detta med något av följande '
seo-description: 'Du måste konfigurera serveregenskaperna så att de återspeglar din miljö. Du kan göra detta med något av följande '
seo-title: Tillämpa egenskaper på servermiljöer
title: Tillämpa egenskaper på servermiljöer
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Tillämpa egenskaper på servermiljöer{#apply-properties-to-server-environments}

Du måste konfigurera serveregenskaperna så att de återspeglar din miljö. Du kan göra detta på något av följande sätt:

* [!DNL flashaccess-i15n.properties] - Exempel som ingår i var och en av  [!DNL .war] filerna

* [!DNL AdobeInitial.properties] - Provet finns i  [!DNL /shared] mappen på dvd-skivan

   Du kan använda den här filen för att åsidosätta egenskaperna som anges i WAR-filen enligt följande:

   1. Ange åsidosättningsegenskapsvärden i [!DNL AdobeInitial.properties]
   1. Placera [!DNL AdobeInitial.properties] i klassökvägen.

   >[!NOTE]
   >
   >Adobe rekommenderar att du använder filen [!DNL AdobeInitial.properties] eftersom du då kan uppdatera WAR-filer i programmet utan att riskera att förlora tidigare egenskapskonfigurationskonfigurationsinställningar som du har gjort i filen [!DNL flashaccess-i15n.properties].

* Egenskapsmekanismen för Java System.

Du kan använda enskilda egenskaper i dessa specifika servermiljöer:

* *Utveckling*
* *Mellanlagring*
* *Produktion*

Med den här funktionen kan du använda samma WAR-fil för alla servermiljöer. Om du vill använda egenskaper i specifika miljöer lägger du till två understreck (&#39; `__`&#39;) plus en av följande miljökoder i egenskapen *name*:

    *`DEV`
    *`STAGE`
    *`PROD

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Om du till exempel vill ställa in loggnivån på `INFO` för dina produktions- och mellanlagringsservrar och på `DEBUG` för utvecklingsservern:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

Servern använder den här sökordningen för egenskaper:

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` i Java-systemegenskaper
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` i Java-systemegenskaper

>[!NOTE]
>
>Du måste ange serverns miljönamn som en Java-systemegenskap när du startar servern. Om du till exempel startar Tomcat med [!DNL catalina.bat] anger du miljövariabeln `CATALINA_OPTS` enligt följande:
>-DENVIRONMENT_NAME=[ DEV | SCEN | PROD ]
