---
title: Konfigurera Tomcat
description: Konfigurera Tomcat
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Konfigurera Tomcat{#configure-tomcat}

På Individualization-servern ändrar du Tomcat-s [!DNL conf/server.xml] -fil som ska innehålla ytterligare information i åtkomstloggen. Du kan använda den här informationen för rapportering.

1. Leta reda på konfigurationen för `AccessLogValve` in [!DNL server.xml] och ändra mönstret så som visas här:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrerar värdet för `x-forwarded-for` header. Om du använder en omvänd Apache-proxy för att vidarebefordra begäranden till Tomcat-servern, innehåller den här rubriken den ursprungliga klientens IP-adress, medan `%h` registrerar Apache-serverns IP-adress. `%{request-id}r` registrerar begärandeidentifieraren, som motsvarar det begärande-ID som finns i Individualization-programloggen.

1. Redigera [!DNL conf/server.xml] och ange `unpackwars` egenskapen är false.

   För både Individualization- och Key Generation-servrar är det en bra idé att redigera [!DNL conf/server.xml] och ange `unpackwars` egenskap till `false`. Om du uppdaterar WAR-filerna måste du kanske även rensa de opackade WAR-mapparna.

>[!NOTE]
>
>Framtida DRM-klienter kräver att du aktiverar och konfigurerar CORS-filtret (Cross-Origin Resource Sharing) som är tillgängligt för Tomcat. Inga DRM-klienter har för närvarande detta krav.
