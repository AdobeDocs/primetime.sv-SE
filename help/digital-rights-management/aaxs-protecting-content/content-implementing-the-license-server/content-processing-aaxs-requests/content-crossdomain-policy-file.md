---
title: Policyfil för korsdomän
description: Policyfil för korsdomän
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Policyfil för korsdomän {#crossdomain-policy-file}

Om licensservern finns på en annan domän än SWF för videouppspelning krävs en korsdomänprincipfil (crossdomain.xml) för att SWF ska kunna begära licenser från licensservern. En korsdomänprincipfil är en XML-fil som gör att servern kan ange att dess data och dokument är tillgängliga för SWF-filer som hanteras från andra domäner. Alla SWF-filer som hanteras från en domän som anges i licensserverns korsdomänprincipfil har åtkomst till data eller resurser från den licensservern.

Adobe rekommenderar att utvecklare följer vedertagna standarder när de distribuerar korsdomänprincipfilen genom att endast tillåta betrodda domäner att komma åt licensservern och begränsa tillgången till licensunderkatalogen på webbservern.

Mer information om korsdomänprincipfiler finns på följande platser:

* Webbplatsinställningar (principfiler)
* Korspolicyfilsspecifikation: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
