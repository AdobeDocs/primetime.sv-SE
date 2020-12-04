---
seo-title: Översikt över nätverkstopologin
title: Översikt över nätverkstopologin
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
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