---
title: Begär certifikat
description: Begär certifikat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Begär certifikat{#requesting-certificates}

Registrering är processen att begära ett certifikat från Adobe. Du kan generera dina nycklar och skapa en begäran som skickas till Adobe. Adobe genererar sedan certifikatet och skickar tillbaka det till dig. Adobe vet inte vad den privata nyckeln innehåller. Därför måste du ha ett sätt att säkerhetskopiera nyckeln så att du kan återställa den om maskinvarufel uppstår.

Till skillnad från licensservern, paketeraren eller transportcertifikatet utfärdas inte domänkontrollantcertifikatet av Adobe. Du kan hämta det här certifikatet från en certifikatutfärdare eller så kan du generera ett självsignerat certifikat.

Instruktioner om hur du får inloggningsuppgifterna för Adobe Access finns i *Adobe Access Certificate Enrollguide*.
