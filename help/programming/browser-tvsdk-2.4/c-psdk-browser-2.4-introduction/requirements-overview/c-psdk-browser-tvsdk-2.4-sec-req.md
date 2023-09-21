---
description: Det finns vissa säkerhetsfrågor att tänka på när det gäller webbläsarens TVSDK.
title: Säkerhetsaspekter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Säkerhetsaspekter{#security-considerations}

Det finns vissa säkerhetsfrågor att tänka på när det gäller webbläsarens TVSDK.

* **Adobe Flash Player**

   * Flashen Player tillåter inte åtkomst till data som finns utanför den domän som SWF kommer från.

     Om du vill tillåta åtkomst ska du ha en korsdomänprincipfil med lämpliga behörigheter i roten på den server där data lagras. I läget för återställning av Flash i webbläsarens TVSDK (Flash Player version 23 och senare) behöver du en autentiseringstoken för din domän. Kontakta din Adobe-representant om du vill generera token.

* **JavaScript**

   * JavaScript följer samma ursprungsprincip och förhindrar åtkomst till resurser över domängränser.

     Om du vill tillåta åtkomst till de här resurserna måste du ange rubriken Access-Control-Allow-Origin (CORS) för de resurser som finns på andra platser än spelaren. Om innehållet anges med hjälp av byteintervall kan CORS preflight-alternativbegäran även ange att dessa begäranden tillåts av ursprunget.

* **Webbläsare och blandat innehåll**

   * Webbläsare kräver att AES-128-krypterat innehåll lagras över säker ursprung (till exempel HTTPS).

     Eftersom de flesta webbläsare inte tillåter blandat innehåll rekommenderar vi att spelaren, innehållet och tillhörande resurser som Key-/WebVTT-filer också lagras via säker origin.

     >[!IMPORTANT]
     >
     >Från och med version 2.4.5 konverteras HTTP-anropen till HTTPS om spelaren lagras via HTTPS med Browser TVSDK när MSE-teknik används.
