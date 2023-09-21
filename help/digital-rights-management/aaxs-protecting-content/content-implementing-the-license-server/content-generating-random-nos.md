---
title: Generera slumpmässiga tal
description: Generera slumpmässiga tal
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Generera slumpmässiga tal{#generating-random-numbers}

Maskinvarubaserade talgeneratorer kan användas på Linux-servrar för att säkerställa att tillräcklig entropi genereras. Om datorn inte kan generera tillräckligt med entropi kommer Adobe Access-åtgärder som kräver en källa för slumpmässighet att blockeras medan data väntar från `/dev/random`.
