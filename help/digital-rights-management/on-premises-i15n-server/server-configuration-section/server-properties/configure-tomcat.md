---
seo-title: Konfigurera Tomcat
title: Konfigurera Tomcat
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Konfigurera Tomcat{#configure-tomcat}

På Individualization-servern ändrar du Tomcat- [!DNL conf/server.xml] -filen så att den innehåller ytterligare information i åtkomstloggen. Du kan använda den här informationen för rapportering.

1. Leta reda på konfigurationen för `AccessLogValve` i [!DNL server.xml] och ändra mönstret som visas här:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` kommer att registrera värdet för `x-forwarded-for` rubriken. Om du använder en omvänd Apache-proxy för att vidarebefordra begäranden till Tomcat-servern, kommer den här rubriken att innehålla den ursprungliga klientens IP-adress, medan `%h` Apache-serverns IP-adress registreras. `%{request-id}r` registrerar begärandeidentifieraren, som motsvarar det begärande-ID som finns i Individualization-programloggen.

1. Redigera [!DNL conf/server.xml] och ange egenskapen `unpackwars` till false.

   För både Individualization- och Key Generation-servrarna är det en bra idé att redigera [!DNL conf/server.xml] och ställa in `unpackwars` egenskapen på `false`. Om du uppdaterar WAR-filerna måste du kanske även rensa de opackade WAR-mapparna.

>[!NOTE]
>
>Framtida DRM-klienter kräver att du aktiverar och konfigurerar CORS-filtret (Cross-Origin Resource Sharing) som är tillgängligt för Tomcat. Inga DRM-klienter har för närvarande detta krav.

