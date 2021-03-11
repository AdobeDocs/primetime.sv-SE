---
title: Översikt över nätverkstopologin
description: Översikt över nätverkstopologin
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Översikt {#network-topology-overview}

När du har distribuerat Adobe Primetime DRM måste du upprätthålla säkerheten för Primetimes DRM-produktionsserver.

>[!NOTE]
>
>Primetime DRM kallades tidigare Adobe Access och tidigare Flash Access.

Du kan använda en *omvänd proxy* för att se till att olika uppsättningar URL:er för Primetime DRM-webbprogram är tillgängliga för externa och interna användare. *Omvänd* proxy är säkrare än att tillåta användare att ansluta direkt till den programserver som Primetime DRM körs på, och den här konfigurationen utför alla HTTP-begäranden för den programserver som kör Primetime DRM. Användare har bara åtkomst till omvänd proxy och kan bara försöka med de URL-anslutningar som stöds av den omvända proxyn.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)