---
title: Ökning
description: Ökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Ökning{#overview}

Du kan behöva återkalla en kunds autentiseringsuppgifter eller kontrollera om en viss uppsättning autentiseringsuppgifter redan har återkallats under vissa villkor. Autentiseringsuppgifterna kan återkallas om de komprometteras. När dessa problem uppstår utfärdas inte längre licenser till kunder som komprometterats.

Adobe har listor över återkallade certifikat (CRL:er) för återkallande av skadade klienter. Dessa listor över återkallade certifikat används automatiskt av SDK:n. Licensservrar kan begränsa klienterna ytterligare genom att inte tillåta vissa datorautentiseringsuppgifter eller särskilda versioner av DRM och körningsreferenser. A `RevocationList` kan skapas och skickas till SDK för att återkalla autentiseringsuppgifter för datorn. Vissa DRM-/runtime-versioner kan återkallas antingen på DRM-principnivå genom att modulbegränsningar anges i uppspelningsrättigheten eller globalt genom att modulbegränsningar anges i `HandlerConfiguration`.

Diskussionen fokuseras på att återkalla klientautentiseringsuppgifter.
