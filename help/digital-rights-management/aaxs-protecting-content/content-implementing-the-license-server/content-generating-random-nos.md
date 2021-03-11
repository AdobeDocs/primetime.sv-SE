---
title: Generera slumpmässiga tal
description: Generera slumpmässiga tal
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# Genererar slumpmässiga tal{#generating-random-numbers}

Maskinvarubaserade talgeneratorer kan användas på Linux-servrar för att säkerställa att tillräcklig entropi genereras. Om datorn inte kan generera tillräckligt mycket entropi kommer Adobe Access-åtgärder som kräver en slumpmässig källa att blockeras medan data från `/dev/random` väntar.
