---
title: Tillåt listning av icke-SWF-program
description: Tillåt listning av icke-SWF-program
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Icke-SWF-program Tillåt listning {#non-swf-application-isting}

AIR var den första plattformen som fanns i programmet och som gör att det går att ta upp information, samt namnet på den egenskap som du använder i andra program än SWF-tillåtelselista (Adobe AIR, iOS, Android osv.) behåller sitt ursprungliga namn: `policy.allowedAIRApplication.n`. Detta gör att innehållet kan spelas upp av alla program som inte är Flash och som har signerats med ett signeringscertifikat före publiceringen. Detta kallas *program-ID*. Du kan extrahera program-ID:t med verktyget [!DNL AdobePublisherIDUtility.jar]. Listan över tillåtna användare används på alla klienter som stöder Primetime DRM.

Program-ID härleds från den offentliga nyckeln för signeringscertifikatet som används för att signera ett visst program. Om den offentliga nyckeln i certifikatet någonsin upphör att gälla, kommer allt tidigare innehåll i listan bara att spelas upp på program som signerats med det gamla certifikatet inte att spelas upp på den nya appen (som signerats med det nya certifikatet).

Om du befinner dig i en situation där du har ett innehållsbibliotek som tillåter listade program som signerades med ett visst signeringscertifikat, och det certifikatet upphör att gälla och du får ett nytt certifikat (med ett annat offentligt/privat nyckelpar), kommer ditt gamla innehåll inte att spelas upp i din nya app *såvida du inte* gör något av följande:

* Använd en `PolicyUpdateList` på licensservern för att åsidosätta den inkommande principen och infoga en ny Application Tillåtelselista-post med det nya signeringscertifikatets sammanfattning.
* Uppdatera licensserverns logik för att åsidosätta den inkommande principen och infoga en ny Application Tillåtelselista-post.
* Begär att utfärdaren av ditt signeringscertifikat utfärdar ett nytt certifikat som använder samma offentliga/privata nyckelpar som det tidigare certifikatet använde.
* Om du levererar HDS/HLS-innehåll som refererar till en URL-slutpunkt för att hämta `DRMMetadata`, kan du återskapa `DRMMetadata` (med Primetime DRM Java SDK) och infoga en ny DRM-princip som innehåller en uppdaterad Application Tillåtelselista-post.

* Paketera om allt ditt gamla innehåll med en ny DRM-princip som har sammanfattningen av ditt nya signeringscertifikat.

Mer information finns i `policy.allowedAIRApplication.n` i *Konfigurationsegenskaper*.

>[!NOTE]
>
>Du måste ha en särskild inställning för att kunna visa upp ett iOS-program. Se [Tillåtelselista ditt iOS-program](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) i *TVSDK for iOS Programmer&#39;s Guide*.
