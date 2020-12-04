---
seo-title: Översikt
title: Översikt
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Översikt{#overview}

Du kan behöva återkalla en kunds autentiseringsuppgifter eller kontrollera om en viss uppsättning autentiseringsuppgifter redan har återkallats under vissa villkor. Autentiseringsuppgifterna kan återkallas om de komprometteras. När dessa problem uppstår utfärdas inte längre licenser till kunder som komprometterats.

Adobe har listor över återkallade certifikat (CRL:er) för återkallande av skadade klienter. Dessa listor över återkallade certifikat används automatiskt av SDK:n. Licensservrar kan begränsa klienterna ytterligare genom att inte tillåta vissa datorautentiseringsuppgifter eller särskilda versioner av DRM och körningsreferenser. Ett `RevocationList`-värde kan skapas och skickas till SDK för att återkalla autentiseringsuppgifter för datorn. Vissa DRM-/runtime-versioner kan återkallas antingen på DRM-principnivå genom att modulbegränsningar anges i uppspelningsrättigheten eller globalt genom att modulbegränsningar anges i `HandlerConfiguration`.

Diskussionen fokuseras på att återkalla klientautentiseringsuppgifter.
