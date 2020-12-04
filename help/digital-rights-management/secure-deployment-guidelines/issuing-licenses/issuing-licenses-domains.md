---
description: För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.
seo-description: För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.
seo-title: Hantera domäner
title: Hantera domäner
uuid: 30b73e38-d6ed-43c6-89ba-ae8616383779
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Hantera domäner {#managing-domains}

För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.

Här är några domänhanteringsmetoder:

* Begränsa den tid som domänens autentiseringsuppgifter är giltiga.

   Klienter måste kontakta domänservern för att återfå domänens autentiseringsuppgifter när de upphör att gälla. Vid den tidpunkten kan domänservern verifiera att datorn fortfarande är auktoriserad att vara medlem i domänen.
* För pekaren över domännycklarna varje gång en användare avregistrerar sig.

   Licensservern bör endast utfärda licenser till klienter som har den senaste domännyckeln. I det här tillvägagångssättet förutsätts att licensservern kan samordna med domänservern för att ta reda på vilken nyckel som är den senaste. När du rullar över domännycklarna måste du generera ett nytt nyckelpar för domänen. När du för pekaren över nycklarna för en domän ökar du nyckelversionen i `generateDomainCredential`.
* Om domänservern är densamma som licensservern kan servern använda återställningsräknaren för att identifiera en säkerhetskopia och återställning.

   Mer information finns i [Bearbeta Adobe Primetime DRM-begäranden](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

