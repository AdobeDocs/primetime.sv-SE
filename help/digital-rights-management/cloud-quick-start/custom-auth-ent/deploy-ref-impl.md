---
title: Distribuera BEES-referensimplementeringen
description: Distribuera BEES-referensimplementeringen
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
