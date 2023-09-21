---
title: Konfigurera sökväg och klassökväg
description: Konfigurera sökväg och klassökväg
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Konfigurera sökväg och klassökväg{#configure-the-path-and-classpath}

The [!DNL flashaccess.war] innehåller [!DNL jsafeWithNative.jar], som är Crypto-J-biblioteket. För det senare krävs ytterligare ett systemspecifikt bibliotek för att utföra krypteringsåtgärder.

1. Lägg till det inbyggda [!DNL jsafe] Bibliotek till din sökväg.

   * **Linux / [!DNL libjsafe.so] -** Katalogen som innehåller [!DNL libjsafe.so] måste finnas på sökvägen (interna Crypto-J-bibliotek är också tillgängliga för andra plattformar). Ange till exempel [!DNL libjsafe.so] på `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** Motparten i Windows till [!DNL libjsafe.so] är lämplig [!DNL jsafe.dll].

   Dessa bibliotek är tillgängliga för dig i [!DNL thirdparty] biblioteksmapp.
1. Placera en av [!DNL adobe-flashaccess-certs] burkar filer i klassökvägen.

       Den här JAR-filen ingår inte i WAR-filen. Du måste lägga till den explicit i klassökvägen.
   
   * Utvecklingsservrar - ska endast användas [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Produktionsservrar - ska endast användas [!DNL adobe-flashaccess- certs.jar]

Distributionen innehåller en [!DNL shared] som innehåller både jar-filen och en förkonfigurerad [!DNL AdobeInitial.properties] -fil. Adobe rekommenderar att du lägger till dessa objekt i `common.loader` via [!DNL catalina.properties] -fil. Till exempel:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
