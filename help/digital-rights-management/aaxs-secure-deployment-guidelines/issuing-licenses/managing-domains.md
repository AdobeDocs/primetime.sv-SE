---
seo-title: Hantera domäner
title: Hantera domäner
uuid: aee02196-8704-46ee-add9-82b371722f0f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Hantera domäner{#managing-domains}

För att förhindra att användare kan säkerhetskopiera och återställa sina filer i ett försök att kringgå domänavregistrering rekommenderar vi att någon av följande metoder implementeras för domänhantering:

* Begränsa den tid som domänens autentiseringsuppgifter är giltiga. Klienter måste kontakta domänservern för att återfå domänens autentiseringsuppgifter när de upphör att gälla. Då kan domänservern se till att datorn fortfarande är behörig att vara medlem i domänen.
* Överför domännycklarna varje gång en användare avregistrerar. Licensservern bör endast utfärda licenser till klienter som har den senaste domännyckeln. Detta förutsätter att licensservern kan samordna med domänservern för att ta reda på vilken nyckel som är den senaste. När du rullar över domännycklarna måste du generera ett nytt nyckelpar för domänen. När du för pekaren över nycklarna för en viss domän måste du öka nyckelversionen i `generateDomainCredential`. Mer information om hur du implementerar en nyckelrollover finns i *RefImplDomainReqHandler* i referensimplementeringen.
* Om domänservern är densamma som licensservern kan servern använda återställningsräknaren för att identifiera säkerhetskopiering och återställning. Se *Bearbeta Adobe Access-begäranden *in *Använda Adobe Access SDK för att skydda innehåll.*

