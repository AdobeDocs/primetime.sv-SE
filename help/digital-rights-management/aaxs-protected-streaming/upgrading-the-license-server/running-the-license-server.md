---
description: Om du vill uppgradera en server som kör Adobe Access Server för skyddad direktuppspelning ersätter du filen flashaccess.war som är distribuerad på programservern med filen som ingår i den senaste Adobe Access-filen. Om du vill använda de nya konfigurationsalternativen som beskrivs ovan uppdaterar du serverns flashaccess-tenant.xml. Du måste också uppdatera jsafe.dll eller libjsafe.so till den version som ingår i den senaste Adobe Access-versionen.
title: Köra Adobe Access Server för skyddad strömning
exl-id: 02ba87c9-d4ec-4d39-926e-5d98b1858349
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Köra Adobe Access Server för skyddad strömning{#running-the-adobe-access-server-for-protected-streaming}

Om du vill uppgradera en server som kör Adobe Access Server för skyddad direktuppspelning ersätter du filen flashaccess.war som är distribuerad på programservern med filen som ingår i den senaste Adobe Access-filen. Om du vill använda de nya konfigurationsalternativen som beskrivs ovan uppdaterar du serverns flashaccess-tenant.xml. Du måste också uppdatera jsafe.dll eller libjsafe.so till den version som ingår i den senaste Adobe Access-versionen.

Innan du kör Adobe Access Server för skyddad direktuppspelning rekommenderar Adobe att du kontrollerar att konfigurationsfilerna är giltiga med de verktyg som finns i licensservern. Mer information finns i &quot;[Konfigurationsvaliderare](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Starta Tomcat och licensservern genom att köra &quot;catalina.bat start&quot; eller &quot;catalina.sh start&quot; från Tomcat&#39;s bin-katalog.

När servern har startats kontrollerar du att den har konfigurerats korrekt genom att öppna *https:// license-server-host:port/flashaccesserver/tenant-name/flashaccess/license/v1* i ett webbläsarfönster. Om klientkonfigurationen lästes in visas ett bekräftelsemeddelande.
