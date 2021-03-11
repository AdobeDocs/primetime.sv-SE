---
title: Kontrollera om licensservern har startats korrekt
description: Kontrollera om licensservern har startats korrekt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Kontrollera om licensservern startade korrekt {#check-whether-the-license-server-started-properly}

Det finns flera sätt att avgöra om din Reference Implementation License Server har startats korrekt. Ett sätt är att kontrollera [!DNL catalina.log]-loggarna, men detta kanske inte är tillräckligt eftersom licensservern loggar in på sina egna loggfiler.
1. Kontrollera din [!DNL AdobeFlashAccess.log]-fil.

   Här skriver Reference Implementation-licensservern logginformation. Platsen för den här loggfilen anges av din [!DNL log4j.xml]-fil och kan ändras så att den pekar på valfri plats. Som standard kopieras loggfilen till arbetskatalogen där du kör ditt `catalina` Tomcat-skript.
1. Gå till följande URL och kontrollera att texten &quot;License Server is Setup correctly&quot; (License Server är korrekt konfigurerad) visas:
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
