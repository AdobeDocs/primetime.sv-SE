---
description: Med den kreativa ompaketeringstjänsten (CRS) kan en annan typ av skribent spelas upp korrekt i HLS-strömmar. Manifestservern anropar CRS när en annons som inte är HLS påträffas.
seo-description: Med den kreativa ompaketeringstjänsten (CRS) kan en annan typ av skribent spelas upp korrekt i HLS-strömmar. Manifestservern anropar CRS när en annons som inte är HLS påträffas.
seo-title: Översikt över CRS
title: Översikt över CRS
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: 4788a8de8ba47d7f448967066e1bd0fb73fdb7a8
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Översikt över CRS {#overview-of-crs}

Med den kreativa ompaketeringstjänsten (CRS) kan en annan typ av skribent spelas upp korrekt i HLS-strömmar. Manifestservern anropar CRS när en annons som inte är HLS påträffas.

>[!NOTE]
>
>CRS är som standard inaktiverat. Om du vill aktivera CRS för ditt konto kontaktar du den tekniska kontohanteraren för Adobe.
>
>Mer information om hur du aktiverar CRS i TVSDK-program finns i *Aktivera CRS i TVSDK-program* i Programmerarens handbok för plattformen. För Android 3.4, se [Aktivera CRS i TVSDK-program](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS förbereder HTTP Live Streaming (HLS) och andra kreatörer för innehållsströmmen och injicerar ID3-paket för annonsspårning på klientsidan. Den konverterar MP4-, FLV- och WebM-filer som tagits emot från annonsservrar, annonsnätverk och myndighetsservrar till HLS-format.

När Adobe Primetime annonsinfogning stöter på annonsinfogning som inte är HLS och kreativ skickar den till CRS för ompackning, vilket vanligtvis inte tar längre tid än tre minuter. CRS skickar den omkodade annonsen till CDN-servern för framtida bruk. Detta kallas **`just-in-time (JIT) repackaging`**. Du kan också koda om annonsmaterial innan de behövs med [API:t för ompaketering](../../dynamic-ad-insertion/creative-repackaging-service/api-repackage.md). Detta kallas *`asynchronous repackaging`*.

Den tekniska kontohanteraren på Adobe kan också ändra vissa CRS-standardbeteenden om ett annat beteende passar bättre för ditt program. Dessa är:

* Prioritet för annonsformaten.

   Avsnittet `MediaFiles` i ett VAST/VMAP-svar kan innehålla olika `MediaFile`-typer. Som standard väljer manifestservern en enligt en fast uppsättning prioriteringar ( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe kan ändra prioriteter för ditt konto.
* Målvaraktighet för annonsering.

   Manifestservern identifierar målannonsens varaktighet från innehållspellistan och skickar den till CRS. Adobe kan ändra det här beteendet så att CRS alltid använder en fast varaktighet som du anger för ditt konto.
