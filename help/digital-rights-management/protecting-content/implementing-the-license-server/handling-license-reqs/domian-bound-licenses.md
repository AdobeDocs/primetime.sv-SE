---
title: Utfärdar domänbundna licenser
description: Utfärdar domänbundna licenser
copied-description: true
exl-id: c29e61e5-d05a-4744-9ec8-7508ed814a57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Utfärdar domänbundna licenser{#issuing-domain-bound-licenses}

Om du vill utfärda en licens med hjälp av en DRM-princip som kräver domänregistrering, måste klientens begäran innehålla en giltig domäntoken som utfärdats av den domänserver som anges i principen. När klienten begär en licens inkluderas automatiskt dess domäntoken för alla domänservrar som anges i innehållets metadata som den har registrerat hos dessa domänservrar. Om den valda DRM-principen kräver domänregistrering väljer SDK sedan automatiskt en domäntoken från begäran att binda licensen till eller returnerar ett fel om ingen lämplig domäntoken har hittats.

En domäntoken anses vara giltig om den inte har gått ut och om den utfärdades av en auktoriserad domäncertifikatutfärdare. Licensservern måste ange från vilka domänmyndigheter den sedan accepterar domäntoken genom att konfigurera `HandlerConfiguration.setDomainCAs()`. Om inga domäncertifikatutfärdare har konfigurerats kan licensservern inte utfärda domänbundna licenser.

Om metadata innehåller flera DRM-principer kan licensserverns affärslogik välja en DRM-princip som baseras på om klienten uppvisade en domäntoken. Du kan använda `LicenseRequestMessage.getDomainTokens()` för att avgöra vilka domäner klienten har registrerat sig med.
