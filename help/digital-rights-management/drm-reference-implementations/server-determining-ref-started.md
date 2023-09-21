---
title: Kontrollera om licensservern har startats korrekt
description: Kontrollera om licensservern har startats korrekt
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Kontrollera om licensservern har startats korrekt {#check-whether-the-license-server-started-properly}

Det finns flera sätt att avgöra om din Reference Implementation License Server har startats korrekt. Ett sätt är att kolla [!DNL catalina.log] loggar, men detta kanske inte är tillräckligt eftersom licensservern loggar till sina egna loggfiler.
1. Kontrollera [!DNL AdobeFlashAccess.log] -fil.

   Här skriver Reference Implementation-licensservern logginformation. Platsen för loggfilen anges av din [!DNL log4j.xml] och kan ändras så att den pekar på valfri plats. Som standard kopieras loggfilen till arbetskatalogen där du kör `catalina` Tomcat-manus.
1. Gå till följande URL och kontrollera att texten &quot;License Server is Setup correctly&quot; (License Server är korrekt konfigurerad) visas:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
