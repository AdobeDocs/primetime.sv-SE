---
title: Lista över tillåtna program utanför SWF
description: Lista över tillåtna program utanför SWF
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Lista över tillåtna program utanför SWF {#non-swf-application-isting}

AIR var den första plattformen som fanns i programmet och som gjorde att det gick att ta upp en lista, samt namnet på den egenskap som du använde i program som inte kommer från SWF (Adobe AIR, iOS, Android osv.) behåller sitt ursprungliga namn: `policy.allowedAIRApplication.n`. Detta gör att innehållet kan spelas upp av alla program som inte är Flashar och som har signerats med ett signeringscertifikat före publiceringen. Detta kallas *Program-ID*. Du kan extrahera program-ID med [!DNL AdobePublisherIDUtility.jar] verktyg. Listan över tillåtna användare används på alla klienter som stöder Primetime DRM.

Program-ID härleds från den offentliga nyckeln för signeringscertifikatet som används för att signera ett visst program. Om den offentliga nyckeln i certifikatet någonsin upphör att gälla, kommer allt tidigare innehåll i listan bara att spelas upp på program som signerats med det gamla certifikatet inte att spelas upp på den nya appen (som signerats med det nya certifikatet).

Om du befinner dig i en situation där du har ett innehållsbibliotek som tillåter listade program som signerades med ett visst signeringscertifikat, och det certifikatet upphör att gälla och du får ett nytt certifikat (med ett annat offentligt/privat nyckelpar), kommer ditt gamla innehåll inte att spelas upp i din nya app *såvida inte* du gör något av följande:

* Använd en `PolicyUpdateList` på din licensserver för att åsidosätta den inkommande principen och infoga en ny Application Tillåtelselista-post med det nya signeringscertifikatets sammanfattning.
* Uppdatera licensserverns logik för att åsidosätta den inkommande principen och infoga en ny Application Tillåtelselista-post.
* Begär att utfärdaren av ditt signeringscertifikat utfärdar ett nytt certifikat som använder samma offentliga/privata nyckelpar som det tidigare certifikatet använde.
* Om du levererar HDS/HLS-innehåll som refererar till en URL-slutpunkt för att hämta `DRMMetadata`kan du generera om `DRMMetadata` (med Primetime DRM Java SDK) för att infoga en ny DRM-princip som innehåller en uppdaterad Application Tillåtelselista-post.

* Paketera om allt ditt gamla innehåll med en ny DRM-princip som har sammanfattningen av ditt nya signeringscertifikat.

Se `policy.allowedAIRApplication.n` in *Konfigurationsegenskaper* för mer information.

>[!NOTE]
>
>Du måste ha en särskild inställning för att kunna visa upp ett iOS-program. Se [Tillåtelselista ditt iOS-program](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) i *TVSDK for iOS Programmer&#39;s Guide*.
