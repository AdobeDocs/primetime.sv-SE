---
title: Brandväggsregler
description: Brandväggsregler
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Brandväggsregler{#firewall-rules}

För att få säker åtkomst till Individualization-servern behöver endast vissa programsökvägar visas. Individualiseringsservern måste acceptera begäranden från klienter till följande sökvägar:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Tjänstsökvägar, t.ex. [!DNL /flashaccess/admin/*] (d.v.s. status- och administratörssidor), får endast vara tillgängliga inifrån brandväggen. Inga delar av Key Generation Server ska vara åtkomliga utanför brandväggen.
