---
title: Hantera domäner
description: Hantera domäner
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Hantera domäner{#managing-domains}

För att förhindra att användare kan säkerhetskopiera och återställa sina filer i ett försök att kringgå domänavregistrering rekommenderar vi att någon av följande metoder implementeras för domänhantering:

* Begränsa den tid som domänens autentiseringsuppgifter är giltiga. Klienter måste kontakta domänservern för att återfå domänens autentiseringsuppgifter när de upphör att gälla. Då kan domänservern se till att datorn fortfarande är behörig att vara medlem i domänen.
* Överför domännycklarna varje gång en användare avregistrerar. Licensservern bör endast utfärda licenser till klienter som har den senaste domännyckeln. Detta förutsätter att licensservern kan samordna med domänservern för att ta reda på vilken nyckel som är den senaste. När du rullar över domännycklarna måste du generera ett nytt nyckelpar för domänen. När du håller tangenterna för en viss domän över måste du se till att öka nyckelversionen i `generateDomainCredential`. Mer information om hur du implementerar en nyckelrollover finns i *RefImplDomainReqHandler* i referensimplementeringen.
* Om domänservern är densamma som licensservern kan servern använda återställningsräknaren för att identifiera säkerhetskopiering och återställning. Se *Bearbetar Adobe Access-begäranden *in *Använda Adobe Access SDK för att skydda innehåll.*
