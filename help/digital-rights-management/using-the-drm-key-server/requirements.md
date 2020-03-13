---
seo-title: Krav för att använda Primetime DRM Key Server
title: Krav för att använda Primetime DRM Key Server
uuid: 769f9e10-7a3e-4a38-b30d-18181b666bb4
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Introduktion {#introduction}

Primetime DRM Key Server är en multi-tenant Key Server för fjärr-iOS och/eller leverans av Xbox 360-nycklar. Om Remote Key Delivery är aktiverat i en princip för iOS måste en Primetime DRM Key Server distribueras för att aktivera innehållsuppspelning på iOS-klienter. Primetime DRM Key Server krävs alltid för Xbox 360.

## Krav för att använda Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}

Minimikraven för att använda Primetime DRM Key Server är:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) eller senare. (För att kunna använda HSM i 64-bitars Windows krävs JRE 8)

   >[!NOTE]
   >
   >64-bitars PKCS11 stöds nu i OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)och Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Autentiseringsuppgifter utfärdade av Adobe
* Autentiseringsuppgifter utfärdade av Microsoft (för Xbox 360-klienter)