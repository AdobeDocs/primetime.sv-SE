---
title: Uppdaterar den globala konfigurationsfilen
description: Uppdaterar den globala konfigurationsfilen
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Uppdaterar den globala konfigurationsfilen{#updating-the-global-configuration-file}

HSM-lösenordet i [!DNL flashaccess-global.xml] kan ändras när som helst och ändringarna börjar gälla nästa gång servern läser in konfigurationsfilen igen. Ändringar av elementen&quot;Loggning&quot; och&quot;Caching&quot; läses dock inte in igen. Ändringar i dessa element kräver att servern startas om.
