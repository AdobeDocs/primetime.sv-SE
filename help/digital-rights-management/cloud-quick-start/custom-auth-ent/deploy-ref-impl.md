---
title: Distribuera BEES-referensimplementeringen
description: Distribuera BEES-referensimplementeringen
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# Distribuera BEES-referensimplementeringen {#deploy-the-bees-reference-implementation}

1. Konfigurera Tomcat-programservern. (Se dokumentationen för Tomcat.)
1. Kopiera `[!DNL bees.war]` till Tomcat&#39;s [!DNL webapps/] mapp.
1. Skicka en förfrågan till `https://localhost:8080/bees`.

   Om du ser ett meddelande om att BEES är i drift slutförs distributionen.
1. Aktivera SSL på servern.
