---
title: Policyfil för korsdomän
description: Policyfil för korsdomän
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Korsdomänprincipfil {#crossdomain-policy-file}

Om licensservern finns på en annan domän än SWF-filen för videouppspelning krävs en korsdomänprincipfil (crossdomain.xml) för att SWF-filen ska kunna begära licenser från licensservern. En korsdomänprincipfil är en XML-fil som gör det möjligt för servern att ange att dess data och dokument är tillgängliga för SWF-filer som hanteras från andra domäner. Alla SWF-filer som hanteras från en domän som anges i licensserverns korsdomänprincipfil har behörighet att komma åt data eller resurser från den licensservern.

Adobe rekommenderar att utvecklare följer vedertagna standarder när de distribuerar korsdomänprincipfilen genom att endast tillåta betrodda domäner att komma åt licensservern och begränsa tillgången till licensunderkatalogen på webbservern.

Mer information om korsdomänprincipfiler finns på följande platser:

* Webbplatsinställningar (principfiler)
* Korspolicyfilsspecifikation: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

