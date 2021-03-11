---
description: Om du vill konfigurera Primetime DRM kopierar du filerna från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Dessutom måste du begära ett certifikat från Adobe Systems, Incorporated. Adobe skickar sedan ut flera autentiseringsuppgifter som du använder för att skydda integriteten för ditt paketerade innehåll, licenser och kommunikation mellan klient och server.
title: Konfigurera utvecklingsmiljön
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Konfigurera utvecklingsmiljön {#set-up-your-development-environment}

Om du vill konfigurera Primetime DRM kopierar du filerna från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Dessutom måste du begära ett certifikat från Adobe Systems, Incorporated. Adobe skickar sedan ut flera autentiseringsuppgifter som du använder för att skydda integriteten för ditt paketerade innehåll, licenser och kommunikation mellan klient och server.

Adobe tillhandahåller Primetime DRM SDK på DVD:

1. Kopiera följande filer från [!DNL [DRM DVD]/SDK/] till ditt utvecklingssystem (i din Java-klassökväg):

   * [!DNL adobe-flashaccess-certs.jar] - Innehåller rotcertifikat från Adobe
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

1. (Valfritt) Om du vill ha bättre prestanda kan du aktivera inbyggt stöd för kryptografiska åtgärder genom att kopiera det plattformsspecifika biblioteket från [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] till utvecklingssystemet (kom ihåg att placera platsen på sökvägen):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >32- och 64-bitarsversioner av dessa bibliotek är tillgängliga. Du bör bara använda 64-bitarsversionen om du har ett 64-bitarsoperativsystem och du kör 64-bitarsversionen av Java.

1. (Valfritt) Kopiera `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` till ditt utvecklingssystem om du vill ha information om funktionerna för FMRMS (Adobe Flash Media Rights Management Server) 1.x-kompatibilitet:

   Distribuera endast detta om du tidigare distribuerat FMRMS 1.x och inte vill paketera om det FMRMS-skyddade innehållet. I så fall måste du lägga till det här stödet på licensservern så att den kan hantera gammalt innehåll och klienter.
