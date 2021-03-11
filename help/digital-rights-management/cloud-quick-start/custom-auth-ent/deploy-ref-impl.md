---
title: Distribuera BEES-referensimplementeringen
description: Distribuera BEES-referensimplementeringen
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# Distribuera BES-referensimplementeringen {#deploy-the-bees-reference-implementation}

1. Konfigurera Tomcat-programservern. (Se dokumentationen för Tomcat.)
1. Kopiera `[!DNL bees.war]`-filen till Tomcat-mappen [!DNL webapps/].
1. Skicka en begäran till `https://localhost:8080/bees`.

   Om du ser ett meddelande om att BEES är i drift slutförs distributionen.
1. Aktivera SSL på servern.
