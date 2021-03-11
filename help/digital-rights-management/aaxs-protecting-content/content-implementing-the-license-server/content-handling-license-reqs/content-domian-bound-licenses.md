---
title: Utfärdar domänbundna licenser
description: Utfärdar domänbundna licenser
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Utfärdar domänbundna licenser{#issuing-domain-bound-licenses}

Om du vill utfärda en licens med hjälp av en princip som kräver domänregistrering, måste klientens begäran innehålla en giltig domäntoken som utfärdats av den domänserver som anges i principen. När klienten begär en licens, kommer den automatiskt att inkludera sina domäntoken för alla domänservrar som anges i innehållets metadata, om den har registrerats med dessa domänservrar. Om den valda principen kräver domänregistrering väljer SDK automatiskt en domäntoken från begäran att binda licensen till eller returnerar ett fel om ingen lämplig domäntoken hittades.

En domäntoken anses vara giltig om den inte har gått ut och om den utfärdades av en auktoriserad domäncertifikatutfärdare. Licensservern måste ange de domänutfärdare som den ska acceptera domäntoken från genom att konfigurera `HandlerConfiguration.setDomainCAs()`. Om inga domäncertifikatutfärdare har konfigurerats kan licensservern inte utfärda domänbundna licenser.

Om metadata innehåller flera principer kan licensserverns affärslogik välja en princip baserat på om klienten uppvisade en domäntoken. Använd `LicenseRequestMessage.getDomainTokens()` för att avgöra vilka domäner klienten har registrerat sig med.
