---
cloud: experience-cloud
product: primetime
audience: end-user
user-guide-title: Hjälp om implementering av Primetime Reference
user-guide-description: Helps understand the TVSDK and modify the feature managers to customize your personal player.
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# PSDK 1.4 för Android-referensimplementering {#reference-implementation}

+ [Översikt över implementering av Android-referenser](home.md)
+ Referensimplementering för Primetime {#reference}
   + [Så här använder du implementeringen av Primetimes referens](ref-implementation/how-to-use-ref-player.md)
   + [Referensimplementationsstruktur](ref-implementation/ref-player-structure.md)
   + Så här använder du funktionshanterare {#feature-managers}
      + [Så här använder du funktionshanterare](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Skapar funktionshanterare genom att skicka konfigurationsinformation till MediaPlayer...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Aktivera och inaktivera funktioner med ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Hantera händelser](ref-implementation/using-feature-managers/handling-events.md)
   + Konfigurera utvecklingsmiljön {#setup-dev}
      + [Konfigurera utvecklingsmiljön](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Hämta och konfigurera programvara som krävs](set-up-dev-environment/download-prereqs-android.md)
      + [Bygg Primetimes referensimplementering](set-up-dev-environment/install-the-ref-player-project.md)
   + Utforska koden {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Funktionschefer](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Katalogformat](set-up-dev-environment/exploring-code/catalog-format.md)
      + [JSON-objekt för Primetime-annonser](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [JSON-objekt för direkta annonsbrytningar](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [JSON-objekt för anpassade annonsmarkörer](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [JSON-objekt för berättiganderesurs-ID](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Exempel på JSON-matningsformat](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implementera videouppspelning {#implement-video}
      + [Viktiga åtgärder för videouppspelning](implement-video-playback/video-playback.md)
      + [Aktivera videouppspelning](implement-video-playback/enable-video-playback.md)
      + [Skydd av DRM-innehåll](implement-video-playback/content-protection.md)
   + [Flera bithastigheter](implement-video-playback/mbr.md)
   + Konfigurera en spelare för DVR-uppspelning med annonser {#dvr}
      + [DVR utan annonsinfogning](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [DVR med annonsinfogning](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [Välja en anpassad startpunkt för DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [Ange en anpassad starttid i referensimplementeringen](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Visa QoS-uppspelning och enhetsstatistik](implement-video-playback/qos-statistics.md)
   + Infoga annonser {#insert-ads}
      + [Annonsinfogning](insert-ads/ad-insertion.md)
      + [Annonsinfogningstyper](insert-ads/ad-insertion-types.md)
      + [Lägg till annonser](insert-ads/add-advertising.md)
      + [Relaterad API-dokumentation](insert-ads/aps-callbacks-ad-insertion.md)
   + Ljud med låg bindning {#late-binding-audio}
      + [Översikt](late-binding-audio/late-binding-audio-overview.md)
      + [Integrera ljud med senare bindning](late-binding-audio/aa-enable.md)
      + [Välj ljudspår](late-binding-audio/select-audio-tracks.md)
      + [Relaterad API-dokumentation](late-binding-audio/aa-api-callbacks.md)
   + Rättighetsflöden för Primetime-autentisering {#primetime-authentications}
      + [Översikt](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [Tillståndshanteraren - översikt](paytvpass-entitlement/entitlement-overvivew.md)
      + [Integrera Primetime-autentisering](paytvpass-entitlement/integrate-pass.md)
      + [Konfigurera Adobe Analytics Reporting](paytvpass-entitlement/pass-analytics-setup.md)
      + [Relaterad API-dokumentation](paytvpass-entitlement/pass-apis-callbacks.md)
   + Videoanalys {#video-analytics}
      + [Videoanalys](video-analytics/video-analytics-overview.md)
      + [Skapa Video Analytics Manager](video-analytics/create-video-analytics-manager.md)
      + [Konfigurera videoanalys](video-analytics/configure-video-analytics-manager.md)
      + [Relaterad API-dokumentation](video-analytics/va-apis-callbacks.md)
   + [Skapa ett anpassat användargränssnitt](build-custom-ui.md)
   + [Felsökning](troubleshooting.md)
