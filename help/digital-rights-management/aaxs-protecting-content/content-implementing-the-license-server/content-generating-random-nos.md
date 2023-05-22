---
title: Generera slumpmässiga tal
description: Generera slumpmässiga tal
copied-description: true
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Generera slumpmässiga tal{#generating-random-numbers}

Maskinvarubaserade talgeneratorer kan användas på Linux-servrar för att säkerställa att tillräcklig entropi genereras. Om datorn inte kan generera tillräckligt mycket entropi kommer Adobe Access-åtgärder som kräver en källa för slumpmässighet att blockeras medan data väntar från `/dev/random`.
