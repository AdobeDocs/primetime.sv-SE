---
title: Brandväggsregler
description: Brandväggsregler
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Brandväggsregler{#firewall-rules}

För att få säker åtkomst till Individualization-servern behöver endast vissa programsökvägar visas. Individualiseringsservern måste acceptera begäranden från klienter till följande sökvägar:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Tjänstsökvägar, som [!DNL /flashaccess/admin/*] (dvs. status- och administratörssidor) får endast vara tillgängliga inifrån brandväggen. Inga delar av nyckelgenereringsservern ska nås utanför brandväggen.
