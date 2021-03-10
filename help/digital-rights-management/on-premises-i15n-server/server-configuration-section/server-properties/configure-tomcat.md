---
title: Konfigurera Tomcat
description: Konfigurera Tomcat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Konfigurera Tomcat{#configure-tomcat}

På Individualization-servern ändrar du Tomcat-filen [!DNL conf/server.xml] så att den innehåller ytterligare information i åtkomstloggen. Du kan använda den här informationen för rapportering.

1. Leta reda på konfigurationen för `AccessLogValve` i [!DNL server.xml] och ändra mönstret så som visas här:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` kommer att registrera värdet för  `x-forwarded-for` rubriken. Om du använder en omvänd Apache-proxy för att vidarebefordra begäranden till Tomcat-servern, innehåller den här rubriken den ursprungliga klientens IP-adress, medan `%h` registrerar Apache-serverns IP-adress. `%{request-id}r` registrerar begärandeidentifieraren, som motsvarar det begärande-ID som finns i Individualization-programloggen.

1. Redigera [!DNL conf/server.xml] och ställ in egenskapen `unpackwars` på false.

   För både Individualization- och Key Generation-servrarna är det en bra idé att redigera [!DNL conf/server.xml] och ställa in egenskapen `unpackwars` på `false`. Om du uppdaterar WAR-filerna måste du kanske även rensa de opackade WAR-mapparna.

>[!NOTE]
>
>Framtida DRM-klienter kräver att du aktiverar och konfigurerar CORS-filtret (Cross-Origin Resource Sharing) som är tillgängligt för Tomcat. Inga DRM-klienter har för närvarande detta krav.

