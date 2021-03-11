---
title: DRM-principfil för korsdomän
description: DRM-principfil för korsdomän
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# DRM-principfil för korsdomän {#crossdomain-drm-policy-file}

Om licensservern finns på en annan domän än SWF-filen för videouppspelning behövs en DRM-principfil mellan domäner ( [!DNL crossdomain.xml]) för att SWF-filen ska kunna begära licenser från en licensserver. En DRM-principfil för flera domäner representeras av en XML-fil som gör att servern kan ange att dess data och dokument är tillgängliga för SWF-filer som hanteras från andra domäner. Alla SWF-filer som hanteras från en domän som anges i licensserverns DRM-korsdomänprincipfil har behörighet att komma åt data eller resurser från den licensservern.

Adobe rekommenderar att utvecklare följer vedertagna standarder när de distribuerar korsdomänprincipfilen genom att endast tillåta betrodda domäner att komma åt licensservern och begränsa tillgången till licensunderkatalogen på webbservern.

Mer information om DRM-principfiler mellan domäner finns på följande platser:

* Webbplatsinställningar (DRM-principfiler)
* DRM-principfilsspecifikation för flera domäner: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

