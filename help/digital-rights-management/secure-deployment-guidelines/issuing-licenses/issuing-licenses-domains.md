---
description: För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.
title: Hantera domäner
exl-id: cbf745d2-ba6e-4144-9608-23870bdfe16d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Hantera domäner {#managing-domains}

För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.

Här är några domänhanteringsmetoder:

* Begränsa den tid som domänens autentiseringsuppgifter är giltiga.

   Klienter måste kontakta domänservern för att återfå domänens autentiseringsuppgifter när de upphör att gälla. Vid den tidpunkten kan domänservern verifiera att datorn fortfarande är auktoriserad att vara medlem i domänen.
* För pekaren över domännycklarna varje gång en användare avregistrerar sig.

   Licensservern bör endast utfärda licenser till klienter som har den senaste domännyckeln. I det här tillvägagångssättet förutsätts att licensservern kan samordna med domänservern för att ta reda på vilken nyckel som är den senaste. När du rullar över domännycklarna måste du generera ett nytt nyckelpar för domänen. När du för tangenterna för en domän ökar du nyckelversionen i `generateDomainCredential`.
* Om domänservern är densamma som licensservern kan servern använda återställningsräknaren för att identifiera en säkerhetskopia och återställning.

   Mer information finns i [Bearbetar Adobe Primetime DRM-begäranden](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
