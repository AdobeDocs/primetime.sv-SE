---
title: Konfigurera sökväg och klassökväg
description: Konfigurera sökväg och klassökväg
copied-description: true
exl-id: e6e9f837-4e3d-43e1-971d-3fa0ccaeff39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Konfigurera sökväg och klassökväg{#configure-the-path-and-classpath}

The [!DNL flashaccess.war] innehåller [!DNL jsafeWithNative.jar], som är Crypto-J-biblioteket. För det senare krävs ytterligare ett systemspecifikt bibliotek för att utföra krypteringsåtgärder.

1. Lägg till det inbyggda [!DNL jsafe] till din sökväg.

   * **Linux / [!DNL libjsafe.so] -** Katalogen som innehåller [!DNL libjsafe.so] måste finnas på sökvägen (interna Crypto-J-bibliotek är också tillgängliga för andra plattformar). Ange till exempel [!DNL libjsafe.so] på `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** Motparten i Windows till [!DNL libjsafe.so] är lämplig [!DNL jsafe.dll].
   Dessa bibliotek är tillgängliga för dig i [!DNL thirdparty] biblioteksmapp.
1. Placera en av [!DNL adobe-flashaccess-certs] burkar filer i klassökvägen.

       Denna JAR-fil ingår inte i WAR-filen. du måste lägga till den explicit i klassökvägen.
   
   * Utvecklingsservrar - ska endast användas [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Produktionsservrar - ska endast användas [!DNL adobe-flashaccess- certs.jar]

Distributionen innehåller en [!DNL shared] som innehåller både jar-filen och en förkonfigurerad [!DNL AdobeInitial.properties] -fil. Adobe rekommenderar att du lägger till dessa objekt i `common.loader` via [!DNL catalina.properties] -fil. Till exempel:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
