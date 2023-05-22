---
title: Begär certifikat
description: Begär certifikat
copied-description: true
exl-id: 49021dba-c6e3-4d11-ab11-061c824b30df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Begär certifikat{#requesting-certificates}

Registrering är processen att begära ett certifikat från Adobe. Du kan generera dina nycklar och skapa en begäran som skickas till Adobe. Adobe genererar sedan certifikatet och skickar tillbaka det till dig. Adobe vet inte vad den privata nyckeln innehåller. Därför måste du ha ett sätt att säkerhetskopiera nyckeln så att du kan återställa den om maskinvarufel uppstår.

Till skillnad från licensservern, paketeraren eller transportcertifikatet utfärdas inte domänkontrollantcertifikatet av Adobe. Du kan hämta det här certifikatet från en certifikatutfärdare eller så kan du generera ett självsignerat certifikat.

Instruktioner om hur du får inloggningsuppgifterna för Adobe Access finns i *Adobe Access Certificate Enrollguide*.
