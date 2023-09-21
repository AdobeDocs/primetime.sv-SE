---
title: Krav för att använda Primetime DRM Key Server
description: Krav för att använda Primetime DRM Key Server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Introduktion {#introduction}

Primetime DRM Key Server är en multi-tenant Key Server för fjärradministration av iOS och/eller Xbox 360. Om Remote Key Delivery är aktiverat i en princip för iOS måste en Primetime DRM Key Server distribueras för att aktivera innehållsuppspelning på iOS-klienter. Primetime DRM Key Server krävs alltid för Xbox 360.

## Krav för att använda Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}

Minimikraven för att använda Primetime DRM Key Server är:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) eller senare. (För att kunna använda HSM i 64-bitars Windows krävs JRE 8)

  >[!NOTE]
  >
  >64-bitars PKCS11 stöds nu i OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)och Oracle
* [Apache Tomcat 7](https://tomcat.apache.org)
* Autentiseringsuppgifter utfärdade av Adobe
* Autentiseringsuppgifter utfärdade av Microsoft (för Xbox 360-klienter)
