---
description: Det finns vissa säkerhetsfrågor att tänka på när det gäller webbläsarens TVSDK.
seo-description: Det finns vissa säkerhetsfrågor att tänka på när det gäller webbläsarens TVSDK.
seo-title: Säkerhetsaspekter
title: Säkerhetsaspekter
uuid: 78edf2b0-363c-4ab6-b588-ab4748ee6096
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Säkerhetsaspekter{#security-considerations}

Det finns vissa säkerhetsfrågor att tänka på när det gäller webbläsarens TVSDK.

* **Adobe Flash Player**

   * Flash Player tillåter inte åtkomst till data som finns utanför den domän som SWF-filen kommer från.

      Om du vill tillåta åtkomst ska du ha en korsdomänprincipfil med lämpliga behörigheter i roten på den server där data lagras. I Flash-återställningsläget i webbläsarens TVSDK (Flash Player version 23 och senare) behöver du en autentiseringstoken för din domän. Kontakta din Adobe-representant om du vill generera token.

* **JavaScript**

   * JavaScript följer samma ursprungsprincip och förhindrar åtkomst till resurser över domängränser.

      Om du vill tillåta åtkomst till de här resurserna måste du ange rubriken Access-Control-Allow-Origin (CORS) för de resurser som finns på andra platser än spelaren. Om innehållet anges med hjälp av byteintervall kan CORS preflight-alternativbegäran även ange att dessa begäranden tillåts av ursprunget.

* **Webbläsare och blandat innehåll**

   * Webbläsare kräver att AES-128-krypterat innehåll lagras över säker ursprung (till exempel HTTPS).

      Eftersom de flesta webbläsare inte tillåter blandat innehåll rekommenderar vi att spelaren, innehållet och tillhörande resurser som Key-/WebVTT-filer också lagras via säker origin.

      >[!IMPORTANT]
      >
      >Från och med version 2.4.5 konverteras HTTP-anropen till HTTPS om spelaren lagras via HTTPS med Browser TVSDK när MSE-teknik används.

