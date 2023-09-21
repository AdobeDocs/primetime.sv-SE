---
title: Distributionsalternativ för licensserver
description: Distributionsalternativ för licensserver
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Distributionsalternativ för licensserver{#license-server-deployment-options}

License Server kan distribueras med något av följande alternativ:

* **Adobe Access Server for Protected Streaming** - Den här licensservern är optimerad för direktuppspelning. Du kan till exempel konfigurera servern för Adobe HTTP Dynamic Streaming med Adobe Access. Den här servern kan driftsättas enkelt med mycket liten konfiguration och har stöd för flera innehavare, vilket kan ge en hög skalbarhet. Eftersom den här implementeringen är optimerad för direktuppspelning stöder den inte alla funktioner i Adobe Access. Användarnamn/lösenord-autentisering, domäner och licenssammanlänkning stöds till exempel inte. Användningsreglerna i licenser som utfärdas av den här servern styrs av en serverkonfigurationsfil, som åsidosätter principen som används vid paketeringen. Se *Handbok för skyddad strömning från Adobe Access Server* om du vill ha mer information om de användningsregler som stöds av den här servern.
* **Referensimplementeringslicensserver** — Använd den här konfigurationen som utgångspunkt för en anpassad serverimplementering. Detta är ett exempel på implementering av licensservrar, inklusive källkod, som visar hur du använder API:erna i Adobe Access SDK för att hantera alla typer av förfrågningar och hur du implementerar anpassad affärslogik som stöds av en databas. Användningsreglerna i licenser som utfärdas av den här servern styrs av den princip som är kopplad till innehållet vid paketeringen.
* **Implementering av anpassad server** — Du kan också implementera en egen licensserver med SDK. Informationen i det här kapitlet beskriver de API:er som används för att implementera en licensserver.
