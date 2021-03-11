---
title: Konfigurera sökväg och klassökväg
description: Konfigurera sökväg och klassökväg
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Konfigurera sökväg och klassökväg{#configure-the-path-and-classpath}

[!DNL flashaccess.war] innehåller [!DNL jsafeWithNative.jar], som är Crypto-J-biblioteket. För det senare krävs ytterligare ett systemspecifikt bibliotek för att utföra krypteringsåtgärder.

1. Lägg till det inbyggda [!DNL jsafe]-biblioteket i sökvägen.

   * **Linux /  [!DNL libjsafe.so] -** Katalogen som innehåller  [!DNL libjsafe.so] måste finnas på sökvägen (interna Crypto-J-bibliotek är också tillgängliga för andra plattformar). Ange till exempel [!DNL libjsafe.so] på `LD_LIBRARY_PATH`.

   * **Windows /  [!DNL jsafe.dll] -** Motdelen i Windows  [!DNL libjsafe.so] är lämplig  [!DNL jsafe.dll].
   Dessa bibliotek är tillgängliga i biblioteksmappen [!DNL thirdparty].
1. Placera en av [!DNL adobe-flashaccess-certs]-filerna i klassökvägen.

       Denna JAR-fil ingår inte i WAR-filen. du måste lägga till den explicit i klassökvägen.
   
   * Utvecklingsservrar - ska bara använda [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Produktionsservrar - ska bara använda [!DNL adobe-flashaccess- certs.jar]

Distributionen innehåller en [!DNL shared]-mapp som innehåller både jar-filen och en förkonfigurerad [!DNL AdobeInitial.properties]-fil. Adobe rekommenderar att du lägger till dessa objekt i `common.loader` via filen [!DNL catalina.properties]. Exempel:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


