---
seo-title: Policyfil för korsdomän
title: Policyfil för korsdomän
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Policyfil för korsdomän {#crossdomain-policy-file}

Om licensservern finns på en annan domän än SWF-filen för videouppspelning krävs en korsdomänprincipfil (crossdomain.xml) för att SWF-filen ska kunna begära licenser från licensservern. En korsdomänprincipfil är en XML-fil som gör det möjligt för servern att ange att dess data och dokument är tillgängliga för SWF-filer som hanteras från andra domäner. Alla SWF-filer som hanteras från en domän som anges i licensserverns korsdomänprincipfil har behörighet att komma åt data eller resurser från den licensservern.

Adobe rekommenderar att utvecklare följer vedertagna standarder när de distribuerar korsdomänprincipfilen genom att endast tillåta betrodda domäner att komma åt licensservern och begränsa tillgången till underkatalogen license på webbservern.

Mer information om korsdomänprincipfiler finns på följande platser:

* Webbplatsinställningar (principfiler)
* Korspolicyfilsspecifikation: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

