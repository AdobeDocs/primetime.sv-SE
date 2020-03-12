---
seo-title: Uppdaterar den globala konfigurationsfilen
title: Uppdaterar den globala konfigurationsfilen
uuid: f733550c-46c0-49c2-8fd1-15906f7d7b22
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppdaterar den globala konfigurationsfilen{#updating-the-global-configuration-file}

HSM-lösenordet i [!DNL flashaccess-global.xml] kan ändras när som helst och ändringarna börjar gälla nästa gång servern läser in konfigurationsfilen igen. Ändringar av elementen&quot;Loggning&quot; och&quot;Caching&quot; läses dock inte in igen. Ändringar i dessa element kräver att servern startas om.
