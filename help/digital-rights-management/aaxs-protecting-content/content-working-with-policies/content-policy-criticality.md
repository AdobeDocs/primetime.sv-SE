---
seo-title: Kritisk politik
title: Kritisk politik
uuid: 076f386e-ba58-4507-92a3-a190126c881e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Kritisk politik{#policy-criticality}

Om nya användningsregler används i profilerna och dessa profiler används i innehåll som paketerats för äldre licensservrar (som inte förstår de nya användningsreglerna), kan du ange hur äldre licensservrar ska fungera. Standardinställningen är att principens kritikalitet är&quot;true&quot;, vilket innebär att licensservern måste förstå alla delar av profilen för att kunna generera en licens med hjälp av principen. Om principens kritikalitet är inställd på &quot;false&quot; kan en äldre licensserver ignorera delar av profilen som den inte förstår, och licenser som genereras av servern kommer inte att innehålla de nya användningsreglerna.

Adobe Access-servrar som använder version 2.0.2 av SDK och senare kommer att respektera inställningen för principkritiska inställningar.
