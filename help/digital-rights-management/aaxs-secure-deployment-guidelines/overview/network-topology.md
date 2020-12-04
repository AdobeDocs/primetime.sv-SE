---
seo-title: Översikt över nätverkstopologin
title: Översikt över nätverkstopologin
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Översikt över nätverkstopologin {#network-topology-overview}

När du har distribuerat Adobe Access är det viktigt att du upprätthåller säkerheten i din miljö. I det här avsnittet beskrivs de åtgärder som krävs för att upprätthålla säkerheten på din Adobe Access-produktionsserver.

Använd en *omvänd proxy* för att se till att olika uppsättningar URL:er för Adobe Access-webbprogram är tillgängliga för både externa och interna användare. Den här konfigurationen är säkrare än att tillåta användare att ansluta direkt till den programserver där Adobe Access körs. Den omvända proxyn utför alla HTTP-begäranden för den programserver som kör Adobe Access. Användare har bara nätverksåtkomst till den omvända proxyn och kan bara försöka med de URL-anslutningar som stöds av den omvända proxyn.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

