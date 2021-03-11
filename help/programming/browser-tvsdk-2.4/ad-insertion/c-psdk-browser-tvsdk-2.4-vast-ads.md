---
description: När webbläsarens TVSDK begär en annons som inte finns på din primära annonsserver, måste spelaren begära annonsen från den sekundära servern. VAST (Video Ad Serving Template) anger kommunikationsstandarden mellan annonsservrar och videospelare och är svaret som skickas av den sekundära annonsservern när annonsen begärs.
title: VAST-annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# VAST-annonser {#vast-ads}

När webbläsarens TVSDK begär en annons som inte finns på din primära annonsserver, måste spelaren begära annonsen från den sekundära servern. VAST (Video Ad Serving Template) anger kommunikationsstandarden mellan annonsservrar och videospelare och är svaret som skickas av den sekundära annonsservern när annonsen begärs.

Mer information om VAST finns i [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

Webbläsarens TVSDK stöder följande VAST-annonselement:

## Radbrytnings- och textbundna annonser {#section_11B8A1A8F52F4F77981C6AAC02185087}

Följande element stöds:

* **`wrapper`** När spelaren behöver kontakta en sekundär annonsserver för att begära en annons, innehåller elementet wrapper omdirigeringsinformationen. Ett wrapper-element kan peka på flera wrapper som pekar på en VAST-annons.

* **`inline`** Följande obligatoriska element stöds:

* `AdSystem`
* `AdTitle`
* `Impression`

   Följande valfria element stöds:

* `Description`
* `Survey`
* `Error`

## Kreatörer {#section_0121F948CB074E49A8132D202786CAA4}

Det här elementet är en fil som är en del av en VAST-annons och innehåller ett `creative`-element som kan hantera en linjär annons, en icke-linjär annons eller en kompletterande annons. I `creative`-elementet stöds elementen `id`, `sequence` och `adId`.

Här finns mer information om annonstyperna:

* **Linjära** annonserFöljande element stöds:

   * `TrackingEvent`, som innehåller  `Tracking` elementet.
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, inklusive följande:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >I det här elementet stöds attributen `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework` och `type`.

* **Icke-linjära** annonserFöljande element stöds:

   * `Non-linear`

      >[!TIP]
      >
      >I det här elementet stöds attributen `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio` och `minSuggestedDuration`.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Tillhörande** annonserFöljande element stöds:

   * `Companion`

      >[!TIP]
      >
      >I det här elementet stöds attributen `id`, `width`, `height`, `apiFramework`, `expandedWidth` och `expandedHeight`.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Tillägg {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Endast Auditude-specifika tillägg stöds.

* `Extension`
