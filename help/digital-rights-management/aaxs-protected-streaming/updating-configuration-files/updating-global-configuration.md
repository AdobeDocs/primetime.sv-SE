---
title: Uppdaterar den globala konfigurationsfilen
description: Uppdaterar den globala konfigurationsfilen
copied-description: true
exl-id: 6544d8ae-6d23-498e-92c5-bad6bfcc10ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Uppdaterar den globala konfigurationsfilen{#updating-the-global-configuration-file}

HSM-lösenordet i [!DNL flashaccess-global.xml] kan ändras när som helst och ändringarna träder i kraft nästa gång servern läser in konfigurationsfilen igen. Ändringar av elementen&quot;Loggning&quot; och&quot;Caching&quot; läses dock inte in igen. Ändringar i dessa element kräver att servern startas om.
