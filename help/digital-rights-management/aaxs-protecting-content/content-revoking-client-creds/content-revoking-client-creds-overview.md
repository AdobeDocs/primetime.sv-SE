---
title: Återkalla klientautentiseringsuppgifter
description: Återkalla klientautentiseringsuppgifter
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Återkalla klientautentiseringsuppgifter{#revoking-client-credentials}

Under vissa omständigheter är det nödvändigt att återkalla en kunds autentiseringsuppgifter eller kontrollera om en viss uppsättning autentiseringsuppgifter redan har återkallats. Autentiseringsuppgifterna kan återkallas om autentiseringsuppgifterna komprometteras. När detta inträffar kommer licenser inte längre att utfärdas till kunder som komprometterats.

Adobe har listor över återkallade certifikat (CRL:er) för återkallande av skadade klienter. Dessa listor över återkallade certifikat används automatiskt av SDK:n. Licensservrar kan begränsa klienterna ytterligare genom att inte tillåta vissa datorautentiseringsuppgifter eller särskilda versioner av DRM och körningsreferenser. A `RevocationList` kan skapas och skickas till SDK för att återkalla autentiseringsuppgifter för datorn. Vissa DRM-/runtime-versioner kan återkallas antingen på principnivå (genom att modulbegränsningar anges i uppspelningsrättigheten) eller globalt (genom att modulbegränsningar anges i `HandlerConfiguration`).

Diskussionen i det här kapitlet kommer att inriktas på att återkalla klientautentiseringsuppgifter.
