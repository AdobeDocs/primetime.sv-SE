---
seo-title: Utfärdar domänbundna licenser
title: Utfärdar domänbundna licenser
uuid: 706650b7-6044-4c01-9f5a-90779127c9e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Utfärdar domänbundna licenser{#issuing-domain-bound-licenses}

Om du vill utfärda en licens med hjälp av en DRM-princip som kräver domänregistrering, måste klientens begäran innehålla en giltig domäntoken som utfärdats av den domänserver som anges i principen. När klienten begär en licens inkluderas automatiskt dess domäntoken för alla domänservrar som anges i innehållets metadata som den har registrerat hos dessa domänservrar. Om den valda DRM-principen kräver domänregistrering väljer SDK sedan automatiskt en domäntoken från begäran att binda licensen till eller returnerar ett fel om ingen lämplig domäntoken har hittats.

En domäntoken anses vara giltig om den inte har gått ut och om den utfärdades av en auktoriserad domäncertifikatutfärdare. Licensservern måste ange från vilka domänmyndigheter den sedan accepterar domäntoken genom att konfigurera `HandlerConfiguration.setDomainCAs()`. Om inga domäncertifikatutfärdare har konfigurerats kan licensservern inte utfärda domänbundna licenser.

Om metadata innehåller flera DRM-principer kan licensserverns affärslogik välja en DRM-princip som baseras på om klienten uppvisade en domäntoken. Du kan använda `LicenseRequestMessage.getDomainTokens()` för att avgöra vilka domäner klienten har registrerat sig med.
