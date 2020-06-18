---
seo-title: Icke-SWF-programvitlista
title: Icke-SWF-programvitlista
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Icke-SWF-programvitlista {#non-swf-application-whitelisting}

AIR var den första plattformen som innehöll programmets vitlista och namnet på den egenskap som du använder för att vitlista andra program än SWF (Adobe AIR, iOS, Android osv.) behåller sitt ursprungliga namn: `policy.allowedAIRApplication.n`. Detta gör att innehållet kan spelas upp av alla icke-Flash-program som har signerats med ett signeringscertifikat före publicering. Detta kallas *program-ID*. Du kan extrahera program-ID:t med [!DNL AdobePublisherIDUtility.jar] verktyget. Den här vitlistningen kommer att tillämpas på alla klienter som stöder Primetime DRM.

Program-ID härleds från den offentliga nyckeln för signeringscertifikatet som används för att signera ett visst program. Om den offentliga nyckeln i certifikatet någonsin förfaller kommer allt tidigare innehåll som visas som vitmarkerat att endast spelas upp i program som signerats med det gamla certifikatet inte att spelas upp i den nya appen (signerat med det nya certifikatet).

Om du befinner dig i en situation där du har ett bibliotek med innehåll som är vitlistat till program som har signerats med ett visst signeringscertifikat, och det certifikatet upphör att gälla och du får ett nytt certifikat (med ett annat offentligt/privat nyckelpar), kommer ditt gamla innehåll inte att spelas upp i din nya app *såvida* du inte gör något av följande:

* Använd en `PolicyUpdateList` på licensservern för att åsidosätta den inkommande principen och infoga en ny vitlistpost för programmet tillsammans med det nya signeringscertifikatets sammanfattning.
* Uppdatera licensserverns logik för att åsidosätta den inkommande principen och infoga en ny vitlistpost för programmet.
* Begär att utfärdaren av ditt signeringscertifikat utfärdar ett nytt certifikat som använder samma offentliga/privata nyckelpar som det tidigare certifikatet använde.
* Om du levererar HDS-/HLS-innehåll som refererar till en URL-slutpunkt för att hämta `DRMMetadata`innehållet, kan du återskapa `DRMMetadata` (med hjälp av Primetime DRM Java SDK) och infoga en ny DRM-princip som innehåller en uppdaterad Application Whitelist-post.

* Paketera om allt ditt gamla innehåll med en ny DRM-princip som har sammanfattningen av ditt nya signeringscertifikat.

Mer information finns `policy.allowedAIRApplication.n` i *Konfigurationsegenskaper* .

>[!NOTE]
>
>Du måste ha en särskild inställning för att kunna visa upp ett iOS-program. Se [Tillåt i listan över iOS-program](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) i *TVSDK for iOS Programmer&#39;s Guide*.
