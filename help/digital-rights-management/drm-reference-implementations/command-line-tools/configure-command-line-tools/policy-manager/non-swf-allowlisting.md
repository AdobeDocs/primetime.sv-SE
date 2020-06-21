---
seo-title: Tillåt listning av icke-SWF-program
title: Tillåt listning av icke-SWF-program
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Tillåt listning av icke-SWF-program {#non-swf-application-allowlisting}

AIR var den första plattformen som applikationen tillät listning på och namnet på egenskapen som du använder för att tillåta listning av program som inte är SWF (Adobe AIR, iOS, Android osv.) behåller sitt ursprungliga namn: `policy.allowedAIRApplication.n`. Detta gör att innehållet kan spelas upp av alla icke-Flash-program som har signerats med ett signeringscertifikat före publicering. Detta kallas *program-ID*. Du kan extrahera program-ID:t med [!DNL AdobePublisherIDUtility.jar] verktyget. Listan över tillåtna användare används på alla klienter som stöder Primetime DRM.

Program-ID härleds från den offentliga nyckeln för signeringscertifikatet som används för att signera ett visst program. Om den offentliga nyckeln i certifikatet någonsin upphör att gälla, kommer allt tidigare innehåll i listan bara att spelas upp på program som signerats med det gamla certifikatet inte att spelas upp på den nya appen (som signerats med det nya certifikatet).

Om du befinner dig i en situation där du har ett innehållsbibliotek som tillåter listade program som signerades med ett visst signeringscertifikat, och det certifikatet upphör att gälla och du får ett nytt certifikat (med ett annat offentligt/privat nyckelpar), kommer ditt gamla innehåll inte att spelas upp i din nya app *såvida* du inte gör något av följande:

* Använd en `PolicyUpdateList` på licensservern för att åsidosätta den inkommande principen och infoga en ny post i listan över tillåtna program med det nya signeringscertifikatets sammanfattning.
* Uppdatera licensserverns logik för att åsidosätta den inkommande principen och infoga en ny post i listan över tillåtna program.
* Begär att utfärdaren av ditt signeringscertifikat utfärdar ett nytt certifikat som använder samma offentliga/privata nyckelpar som det tidigare certifikatet använde.
* Om du levererar HDS-/HLS-innehåll som refererar till en URL-slutpunkt för att hämta `DRMMetadata`filen kan du återskapa `DRMMetadata` (med hjälp av Primetime DRM Java SDK) och infoga en ny DRM-princip som innehåller en uppdaterad post i listan över tillåtna program.

* Paketera om allt ditt gamla innehåll med en ny DRM-princip som har sammanfattningen av ditt nya signeringscertifikat.

Mer information finns `policy.allowedAIRApplication.n` i *Konfigurationsegenskaper* .

>[!NOTE]
>
>Du måste ha en särskild inställning för att kunna visa upp ett iOS-program. Se [Tillåt i listan över iOS-program](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) i *TVSDK for iOS Programmer&#39;s Guide*.
