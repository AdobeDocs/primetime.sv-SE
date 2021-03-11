---
title: Delvis krypteringsnivå
description: Delvis krypteringsnivå
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Delvis krypteringsnivå{#partial-encryption-level}

Anger om alla bildrutor, eller bara en delmängd av bildrutor, ska krypteras. Det finns tre krypteringsnivåer: låg, medel och hög.

>[!NOTE]
>
>Endast för videospår i F4V-/H.264-filer.

Delvis kryptering är utformat för att ge innehållsleverantörer granularitet för att koda innehållet i delar. Kryptering av innehåll lägger till processorkapacitet till den enhet som dekrypterar och visar innehållet. Använd partiell kryptering för att minska CPU-belastningen samtidigt som mycket starkt skydd av innehållet bibehålls. Ett motiverat exempel på hur den här funktionen används är en enda innehållsdel som är avsedd att spelas upp på enheter med låg, medel och hög strömförsörjning.

På grund av videokodningens natur är det inte nödvändigt att kryptera 100 % av videon för att den ska bli ospelbar om den blir stulen. Delvis kryptering har tre inställningar, låg, medel och hög, och de associerade procentsatserna för kryptering beror på hur videon kodas. På grund av det här kodningsberoendet ligger den procentandel av ditt innehåll som är krypterat inom följande intervall:

* Hög: Krypterar alla exempel.
* Medel: Krypterar 50 % av måldata.
* Låg: Krypterar ett mål på 20 till 30 % av data.

De här inställningarna har utformats med följande regel: Allt innehåll som krypteras vid låg inställning krypteras också vid medelhög inställning. Detta garanterar att samma innehåll som distribueras med låg kryptering av en part och distribueras med medelkryptering av en annan part inte äventyrar skyddet av innehållet.

Exempel: Om du minskar krypteringsnivån minskas krypteringsbelastningen på klienten och uppspelningsprestandan förbättras på avancerade datorer.
