---
seo-title: Återkalla klientautentiseringsuppgifter
title: Återkalla klientautentiseringsuppgifter
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Återkalla klientautentiseringsuppgifter{#revoking-client-credentials}

Under vissa omständigheter är det nödvändigt att återkalla en kunds autentiseringsuppgifter eller kontrollera om en viss uppsättning autentiseringsuppgifter redan har återkallats. Autentiseringsuppgifterna kan återkallas om autentiseringsuppgifterna komprometteras. När detta inträffar kommer licenser inte längre att utfärdas till kunder som komprometterats.

Adobe har listor över spärrade certifikat (CRL:er) för återkallande av skadade klienter. Dessa listor över återkallade certifikat används automatiskt av SDK:n. Licensservrar kan begränsa klienterna ytterligare genom att inte tillåta vissa datorautentiseringsuppgifter eller särskilda versioner av DRM och körningsreferenser. En `RevocationList` fil kan skapas och skickas till SDK för att återkalla autentiseringsuppgifter för datorn. Vissa DRM-/runtime-versioner kan återkallas antingen på principnivå (genom att modulbegränsningar anges i uppspelningshöger) eller globalt (genom att modulbegränsningar anges i `HandlerConfiguration`).

Diskussionen i det här kapitlet kommer att inriktas på att återkalla klientautentiseringsuppgifter.
