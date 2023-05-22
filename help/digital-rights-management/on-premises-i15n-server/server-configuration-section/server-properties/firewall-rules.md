---
title: Brandväggsregler
description: Brandväggsregler
copied-description: true
exl-id: 1a40822a-893d-43ec-9c3e-8e0b4ebe6d01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Brandväggsregler{#firewall-rules}

För att få säker åtkomst till Individualization-servern behöver endast vissa programsökvägar visas. Individualiseringsservern måste acceptera begäranden från klienter till följande sökvägar:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Tjänstsökvägar, som [!DNL /flashaccess/admin/*] (dvs. status- och administratörssidor) får endast vara tillgängliga inifrån brandväggen. Inga delar av Key Generation Server ska vara åtkomliga utanför brandväggen.
