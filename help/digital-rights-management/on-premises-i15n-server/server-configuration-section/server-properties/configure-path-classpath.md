---
seo-title: Konfigurera sökväg och klassökväg
title: Konfigurera sökväg och klassökväg
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# Konfigurera sökväg och klassökväg{#configure-the-path-and-classpath}

The [!DNL flashaccess.war] contains [!DNL jsafeWithNative.jar], which is the Crypto-J library. För det senare krävs ytterligare ett systemspecifikt bibliotek för att utföra krypteringsåtgärder.

1. Lägg till det inbyggda [!DNL jsafe] biblioteket i sökvägen.

   * **Linux /[!DNL libjsafe.so]-** Katalogen som innehåller [!DNL libjsafe.so] måste finnas på sökvägen (systemspecifika Crypto-J-bibliotek är också tillgängliga för andra plattformar). Ange till exempel [!DNL libjsafe.so] på `LD_LIBRARY_PATH`.

   * **Windows /[!DNL jsafe.dll]-** Motdelen i Windows till [!DNL libjsafe.so] är lämplig [!DNL jsafe.dll].
   Dessa bibliotek är tillgängliga i [!DNL thirdparty] biblioteksmappen.
1. Lägg en av [!DNL adobe-flashaccess-certs] burkfilerna i klassökvägen.

       Denna JAR-fil ingår inte i WAR-filen. du måste lägga till den explicit i klassökvägen.
   
   * Utvecklingsservrar - ska endast användas [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Produktionsservrar - ska endast användas [!DNL adobe-flashaccess- certs.jar]

Distributionen innehåller en [!DNL shared] mapp som innehåller både jar-filen och en förkonfigurerad [!DNL AdobeInitial.properties] fil. Adobe rekommenderar att du lägger till dessa objekt i `common.loader` via [!DNL catalina.properties] filen. Exempel:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


