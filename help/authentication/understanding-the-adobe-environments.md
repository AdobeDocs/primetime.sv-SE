---
title: Förstå Adobe-miljöer
description: Förstå Adobe-miljöer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Förstå Adobe-miljöer {#understanding-the-adobe-environments}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

Den officiella dokumentationen som beskriver Adobe-miljöerna finns tillgänglig [Konfigurera miljön och testningen i Pre-qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md):

Miljöerna i Adobe, sammanfattas med några ord:

Adobe har två miljöer: **Förkvalificering** och **Frigör**.

* I förkvalificeringsmiljön förbereder vi den nya versionen som ska släppas.

* Den aktuella versionen finns i versionsmiljön.

Varje miljö har två profiler: **mellanlagring** och **produktion**.

* Mellanlagringsprofilen ansluts till MVPD-testservern
* Produktionsprofilen ansluter till produktionsprofilen för videofilmsprogram.

Anledningen till att de två profilerna finns är att vi förbereder nya partners för publicering i staging-profilen, och de vill testa systemet med antingen den kommande versionen (förkvalificering) eller med releasen (mer stabil).

Om en partner vill testa den nya versionen finns det ytterligare några steg som måste utföras. Se, [Konfigurera miljön och testningen i Pre-qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

Genom att följa stegen ovan kan du vara säker på att den kommande releasen kommer att testas i förkvalificeringsmiljön.
