---
description: Om du vill uppgradera en server som kör Adobe Access Server för skyddad direktuppspelning ersätter du filen flashaccess.war som är distribuerad på programservern med filen som ingår i den senaste Adobe Access-filen. Om du vill använda de nya konfigurationsalternativen som beskrivs ovan uppdaterar du serverns flashaccess-tenant.xml. Du måste också uppdatera jsafe.dll eller libjsafe.so till den version som ingår i den senaste Adobe Access-versionen.
seo-description: Om du vill uppgradera en server som kör Adobe Access Server för skyddad direktuppspelning ersätter du filen flashaccess.war som är distribuerad på programservern med filen som ingår i den senaste Adobe Access-filen. Om du vill använda de nya konfigurationsalternativen som beskrivs ovan uppdaterar du serverns flashaccess-tenant.xml. Du måste också uppdatera jsafe.dll eller libjsafe.so till den version som ingår i den senaste Adobe Access-versionen.
seo-title: Köra Adobe Access Server för skyddad strömning
title: Köra Adobe Access Server för skyddad strömning
uuid: 3819500d-ad2f-49eb-8aa4-e50a55461608
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Köra Adobe Access Server för skyddad direktuppspelning{#running-the-adobe-access-server-for-protected-streaming}

Om du vill uppgradera en server som kör Adobe Access Server för skyddad direktuppspelning ersätter du filen flashaccess.war som är distribuerad på programservern med filen som ingår i den senaste Adobe Access-filen. Om du vill använda de nya konfigurationsalternativen som beskrivs ovan uppdaterar du serverns flashaccess-tenant.xml. Du måste också uppdatera jsafe.dll eller libjsafe.so till den version som ingår i den senaste Adobe Access-versionen.

Innan du kör Adobe Access Server för skyddad direktuppspelning rekommenderar Adobe att du kontrollerar att konfigurationsfilerna är giltiga med de verktyg som finns i licensservern. Mer information finns i &quot;[Konfigurationsvaliderare](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Starta Tomcat och licensservern genom att köra &quot;catalina.bat start&quot; eller &quot;catalina.sh start&quot; från Tomcat&#39;s bin-katalog.

När servern har startats kontrollerar du att den är korrekt konfigurerad genom att öppna *https:// license-server-host:port/flashaccesserver/tenant-name/flashaccess/license/v1* i ett webbläsarfönster. Om klientkonfigurationen lästes in visas ett bekräftelsemeddelande.
