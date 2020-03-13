---
description: 'null'
seo-description: 'null'
seo-title: Kontrollera om licensservern har startats korrekt
title: Kontrollera om licensservern har startats korrekt
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Kontrollera om licensservern har startats korrekt {#check-whether-the-license-server-started-properly}

Det finns flera sätt att avgöra om din Reference Implementation License Server har startats korrekt. Ett sätt är att kontrollera [!DNL catalina.log] loggarna, men detta kanske inte är tillräckligt eftersom licensservern loggar till sina egna loggfiler.
1. Kontrollera din [!DNL AdobeFlashAccess.log] fil.

   Här skriver Reference Implementation-licensservern logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml] fil och kan ändras så att den pekar på valfri plats. Som standard kopieras loggfilen till arbetskatalogen där du kör ditt `catalina` Tomcat-skript.
1. Gå till följande URL och kontrollera att texten &quot;License Server is Setup correctly&quot; (License Server är korrekt konfigurerad) visas:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
