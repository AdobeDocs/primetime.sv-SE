---
description: För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.
title: Hantera domäner
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Hantera domäner {#managing-domains}

För att förhindra användare från att säkerhetskopiera och återställa filer för att kringgå domänavregistrering måste du implementera vissa domänhanteringsmetoder.

Här är några domänhanteringsmetoder:

* Begränsa den tid som domänens autentiseringsuppgifter är giltiga.

  Klienter måste kontakta domänservern för att återfå domänens autentiseringsuppgifter när de upphör att gälla. Vid den tidpunkten kan domänservern verifiera att datorn fortfarande är auktoriserad att vara medlem i domänen.
* För över domännycklarna varje gång en användare avregistrerar sig.

  Licensservern bör endast utfärda licenser till klienter som har den senaste domännyckeln. I det här tillvägagångssättet förutsätts att licensservern kan samordna med domänservern för att ta reda på vilken nyckel som är den senaste. När du rullar över domännycklarna måste du generera ett nytt nyckelpar för domänen. När du för tangenterna för en domän ökar du nyckelversionen i `generateDomainCredential`.
* Om domänservern är densamma som licensservern kan servern använda återställningsräknaren för att identifiera en säkerhetskopia och återställning.

  Mer information finns i [Bearbetar Adobe Primetime DRM-begäranden](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
