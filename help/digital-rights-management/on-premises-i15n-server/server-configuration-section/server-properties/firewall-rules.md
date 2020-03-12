---
seo-title: Brandväggsregler
title: Brandväggsregler
uuid: f1629ceb-22de-4bb5-b73f-9b874d97ea8b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Brandväggsregler{#firewall-rules}

För att få säker åtkomst till Individualization-servern behöver endast vissa programsökvägar visas. Individualiseringsservern måste acceptera begäranden från klienter till följande sökvägar:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Tjänstsökvägar, t.ex. [!DNL /flashaccess/admin/*] (t.ex. status- och administratörssidor), får endast vara tillgängliga inifrån brandväggen. Inga delar av Key Generation Server ska vara åtkomliga utanför brandväggen.
