---
title: Roku SSO - översikt
description: Om Roku SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Roku SSO-översikt {#overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#roku-sso-intro}

Det här dokumentet beskriver den information som krävs för att dra nytta av Single Sign On-funktionen på Roku-enheter. Adobe Primetime Authentication samarbetar med Roku för att förbättra användarupplevelsen vid inloggning och för att underlätta enkel inloggning på TV Everywhere-program för TV-prenumeranter.

Lösningen baseras på Adobe Primetime autentiserings klientlösa REST API, så de flesta programmerare behöver inte uppdatera sina program för att kunna använda enkel inloggning.

## Aktivera Roku SSO {#enable-roku-sso}

Roku SSO är aktiverat som standard såvida inte programmeraren eller MVPD-begäran för enkel inloggning har inaktiverats.

Varje programmerare kan aktivera/inaktivera enkel inloggning på Roku-plattformen för specifika integreringar.

### Vad en programmerare bör göra för Roku SSO att fungera {#make-roku-sso-work}

För programmerarprogram som implementerar REST API på klientenheter fungerar Roku SSO utan ändringar. Roku OS lägger till två HTTP-huvuden vid alla förfrågningar till slutpunkterna för Adobe Primetime-autentisering.

För programmerarprogram som implementerar en Server-till-server-lösning för REST api bör programmeraren kontakta Roku-teamet och be om en konfiguration där dessa två rubriker ska skickas till deras domän för alla API-flöden.

Ett nytt prenumerant-ID som används i stället för det enhets-ID som skickas av programmet för att säkerställa enkel inloggning mellan program (och enheter).

Mer information om formatet på sidhuvudena får du av Adobe.

### Möjliga problem {#possible-issues}

Programmerarna bör kontrollera att deras nuvarande implementeringar baserade på Adobe Klientless REST API inte förhindrar Rokus platform-SSO. Nedan finns en lista över möjliga problem och hur de bör lösas.

| Problem | Möjlig orsak | Möjliga lösningar | |-|-|-| |Ingen Roku SSO-rubrik har skickats till Adobe|Använder HTTP i stället för HTTPS för anrop till Adobe Primetime autentiseringsdomäner|Använd HTTPS| |MVPD-logotypen visas inte/har inte uppdaterats för SSO-tokens|Användargränssnittet är beroende av lokal lagring|Program bör uppdatera användargränssnittet (och lokal lagring om det behövs) efter verifiering| |Utloggningen utlöstes inte för AuthZ|Programdesign|Programmet ska uppdateras så att utloggningen aldrig utförs bakom scenerna|

## Vanliga frågor {#faq}

* **Hur fungerar SSO?**

   SSO fungerar i alla programmeringsprogram som drivs av Adobe Primetime-autentisering på alla Roku-enheter som är kopplade till samma Roku-användare.
Roku SSO tillåts inte för alla MVPD-program.

* **Kommer autentiserings-TTL att ändras?**

   Den första giltiga autentiseringstoken används för att utföra enkel inloggning och i det här fallet kommer alla andra program som autentiseras via enkel inloggning att använda samma TTL tills den upphör att gälla. När du navigerar från ett program till ett annat kommer det andra programmet att dela TTL-värdet för det första programmet som autentiseras.

* **Fungerar andra Adobe-funktioner som tidigare?**

   Alla autentiseringsfunktioner i Primetime fungerar som tidigare.

* **Finns det någon process för programmerarens deltagande/avanmälan som drar nytta av enkel inloggning på Roku-plattformen?**

   Detta kommer att bli en konfigurationsändring i Adobe TV Dashboard. Varje programmerare kan aktivera/inaktivera enkel inloggning på Roku-plattformen för specifika integreringar.
