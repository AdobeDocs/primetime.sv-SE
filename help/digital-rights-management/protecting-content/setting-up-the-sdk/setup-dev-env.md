---
description: Om du vill konfigurera Primetime DRM kopierar du filerna från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Dessutom måste du begära ett certifikat från Adobe Systems, Incorporated. Adobe ger dig sedan flera inloggningsuppgifter som du använder för att skydda integriteten för ditt paketerade innehåll, dina licenser och din kommunikation mellan klient och server.
seo-description: Om du vill konfigurera Primetime DRM kopierar du filerna från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Dessutom måste du begära ett certifikat från Adobe Systems, Incorporated. Adobe ger dig sedan flera inloggningsuppgifter som du använder för att skydda integriteten för ditt paketerade innehåll, dina licenser och din kommunikation mellan klient och server.
seo-title: Konfigurera utvecklingsmiljön
title: Konfigurera utvecklingsmiljön
uuid: 68afefe8-7ec6-466e-89a8-bc0da8afb4c8
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Konfigurera utvecklingsmiljön {#set-up-your-development-environment}

Om du vill konfigurera Primetime DRM kopierar du filerna från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Dessutom måste du begära ett certifikat från Adobe Systems, Incorporated. Adobe ger dig sedan flera inloggningsuppgifter som du använder för att skydda integriteten för ditt paketerade innehåll, dina licenser och din kommunikation mellan klient och server.

Adobe tillhandahåller Primetime DRM SDK på DVD:

1. Kopiera följande filer från [!DNL [DRM DVD]/SDK/] till ditt utvecklingssystem (i Java-klassökvägen):

   * [!DNL adobe-flashaccess-certs.jar] - Inkluderar Adobes rotcertifikat
   * [!DNL adobe-flashaccess-sdk.jar] - Innehåller SDK-klasser för Primetime-DRM Core
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Inkluderar Primetime DRM Professional SDK-klasser, som endast krävs för Professional-funktioner

1. Kopiera följande filer från [!DNL [DRM DVD]/SDK/thirdparty] till ditt utvecklingssystem:

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (Valfritt) Om du vill ha förbättrade prestanda kan du aktivera inbyggt stöd för kryptografiska åtgärder genom att kopiera det plattformsspecifika biblioteket från [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] till utvecklingssystemet (kom ihåg att placera platsen på sökvägen):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >32- och 64-bitarsversioner av dessa bibliotek är tillgängliga. Du bör bara använda 64-bitarsversionen om du har ett 64-bitarsoperativsystem och du kör 64-bitarsversionen av Java.

1. (Valfritt) Om du vill ha information om kompatibiliteten med Adobe Flash Media Rights Management Server (FMRMS) 1.x kopierar du `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` till utvecklingssystemet:

   Distribuera endast detta om du tidigare distribuerat FMRMS 1.x och inte vill paketera om det FMRMS-skyddade innehållet. I så fall måste du lägga till det här stödet på licensservern så att den kan hantera gammalt innehåll och klienter.
