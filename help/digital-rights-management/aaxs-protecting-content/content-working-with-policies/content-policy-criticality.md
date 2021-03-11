---
title: Kritisk politik
description: Kritisk politik
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Kritisk princip{#policy-criticality}

Om nya användningsregler används i profilerna och dessa profiler används i innehåll som paketerats för äldre licensservrar (som inte förstår de nya användningsreglerna), kan du ange hur äldre licensservrar ska fungera. Standardinställningen är att principens kritikalitet är&quot;true&quot;, vilket innebär att licensservern måste förstå alla delar av profilen för att kunna generera en licens med hjälp av principen. Om principens kritikalitet är inställd på &quot;false&quot; kan en äldre licensserver ignorera delar av profilen som den inte förstår, och licenser som genereras av servern kommer inte att innehålla de nya användningsreglerna.

Adobe Access-servrar som använder version 2.0.2 av SDK och senare kommer att respektera inställningen för principkritiska inställningar.
