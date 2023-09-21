---
description: När webbläsarens TVSDK begär en annons som inte finns på din primära annonsserver, måste spelaren begära annonsen från den sekundära servern. VAST (Video Ad Serving Template) anger kommunikationsstandarden mellan annonsservrar och videospelare och är svaret som skickas av den sekundära annonsservern när annonsen begärs.
title: VAST-annonser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

Det här elementet är en fil som är en del av en VAST-annons och som innehåller en `creative` -element som har stöd för en linjär annons, en icke-linjär annons eller en kompletterande annons. I `creative` -element, `id`, `sequence`och `adId` -element stöds.

Här finns mer information om annonstyperna:

* **Linjära annonser** Följande element stöds:

   * `TrackingEvent`, som innehåller `Tracking` -element.
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
        >I det här elementet `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`och `type` attribut stöds.

* **Icke-linjära annonser** Följande element stöds:

   * `Non-linear`

     >[!TIP]
     >
     >I det här elementet `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`och `minSuggestedDuration` attribut stöds.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Pressannonser** Följande element stöds:

   * `Companion`

     >[!TIP]
     >
     >I det här elementet `id`, `width`, `height`, `apiFramework`, `expandedWidth`och `expandedHeight` attribut stöds.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Tillägg {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Endast Auditude-specifika tillägg stöds.

* `Extension`
