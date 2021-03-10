---
title: Distributionsalternativ för licensserver
description: Distributionsalternativ för licensserver
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Distributionsalternativ för licensserver{#license-server-deployment-options}

License Server kan distribueras med något av följande alternativ:

* **Adobe Access Server for Protected Streaming**  - Denna licensserver är optimerad för strömning. Du kan till exempel konfigurera servern för Adobe HTTP Dynamic Streaming med Adobe Access. Den här servern kan driftsättas enkelt med mycket liten konfiguration och har stöd för flera innehavare, vilket kan ge en hög skalbarhet. Eftersom den här implementeringen är optimerad för direktuppspelning stöder den inte alla funktioner i Adobe Access. Användarnamn/lösenord-autentisering, domäner och licenssammanlänkning stöds till exempel inte. Användningsreglerna i licenser som utfärdas av den här servern styrs av en serverkonfigurationsfil, som åsidosätter principen som används vid paketeringen. Mer information om vilka användningsregler som stöds av den här servern finns i *Adobe Access Server for Protected Streaming Guide*.
* **Referensimplementeringslicensserver**  - Använd den här konfigurationen som startpunkt för en anpassad serverimplementering. Detta är ett exempel på implementering av licensservrar, inklusive källkod, som visar hur du använder API:erna i Adobe Access SDK för att hantera alla typer av begäranden och hur du implementerar anpassad affärslogik som stöds av en databas. Användningsreglerna i licenser som utfärdas av den här servern styrs av den princip som är kopplad till innehållet vid paketeringen.
* **Anpassad serverimplementering**  - Du kan även implementera en egen licensserver med SDK. Informationen i det här kapitlet beskriver de API:er som används för att implementera en licensserver.

