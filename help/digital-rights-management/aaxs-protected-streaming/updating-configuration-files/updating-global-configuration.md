---
title: Uppdaterar den globala konfigurationsfilen
description: Uppdaterar den globala konfigurationsfilen
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Uppdaterar den globala konfigurationsfilen{#updating-the-global-configuration-file}

HSM-lösenordet i [!DNL flashaccess-global.xml] kan ändras när som helst och ändringarna träder i kraft nästa gång servern läser in konfigurationsfilen igen. Ändringar av elementen Loggning och Caching läses inte in igen. Ändringar i dessa element kräver att servern startas om.
