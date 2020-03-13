---
description: TVSDK kan spela upp videor som har flera profiler med olika bithastigheter och växla mellan dem för att ge mer än en kvalitetsnivå baserat på den tillgängliga bandbredden.
seo-description: TVSDK kan spela upp videor som har flera profiler med olika bithastigheter och växla mellan dem för att ge mer än en kvalitetsnivå baserat på den tillgängliga bandbredden.
seo-title: Flera bithastigheter
title: Flera bithastigheter
uuid: 46eac41e-0b2a-42e3-8a88-54ad9fe34212
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Flera bithastigheter {#multiple-bit-rates}

TVSDK kan spela upp videor som har flera profiler med olika bithastigheter och växla mellan dem för att ge mer än en kvalitetsnivå baserat på den tillgängliga bandbredden.

Du kan ange inledande, lägsta och högsta bithastighet samt adaptiv bithastighet (ABR)-switchprincipen för en ström med flera bithastigheter (MBR). TVSDK växlar automatiskt till den bithastighet som ger den bästa uppspelningsupplevelsen i den angivna konfigurationen.

Referensimplementeringen konfigurerar följande ABR-parametrar i [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| Parameter | Beskrivning |
|--- |--- |
| Inledande bithastighet:  getABRInitialBitRate | Den önskade uppspelningsbithastigheten (i bitar per sekund) för det första segmentet. När uppspelningen startar används den närmaste profilen (lika med eller högre än den ursprungliga bithastigheten) för det första segmentet.  Om en lägsta bithastighet definieras och den inledande bithastigheten är lägre än den lägsta, väljer TVSDK profilen med den lägsta bithastigheten över den lägsta bithastigheten. På samma sätt, om den inledande hastigheten ligger över den högsta nivån, väljer TVSDK den högsta nivån under den högsta. Om den inledande bithastigheten är noll eller odefinierad bestäms den inledande bithastigheten av ABR-principen.  Returnerar ett heltalsvärde som representerar byteprofilen per sekund. |
| Minsta bithastighet:  getABRMinBitRate | Den lägsta tillåtna bithastigheten som ABR kan växla till. ABR-växling ignorerar profiler med en lägre bithastighet än så. Returnerar ett heltalsvärde som representerar bitprofilen per sekund. |
| Maximal bithastighet:  getABRMaxBitRate | Den högsta tillåtna bithastighet som ABR kan växla till. ABR-växling ignorerar profiler med en högre bithastighet än detta. Returnerar ett heltalsvärde som representerar bitprofilen per sekund. |
| Princip för ABR-växling:  getABRPolicy | Uppspelningen växlar gradvis till den högsta bithastigheten när det är möjligt. Du kan ange en princip för ABR-växling, som avgör hur snabbt TVSDK växlar mellan profiler. Standardvärdet är Måttligt. <ul><li>*Konservativ*: Växlar till profilen med nästa högre bithastighet när bandbredden är 50 % högre än den aktuella bithastigheten. </li><li>*Måttlig*: Växlar till nästa högre bithastighetsprofil när bandbredden är 20 % högre än den aktuella bithastigheten.</li><li>*Aggressiv*: Växlar omedelbart till den högsta bithastighetsprofilen när bandbredden är högre än den aktuella bithastigheten</li></ul><br/>Om den inledande bithastigheten är noll eller inte har angetts och en princip anges, startar uppspelningen med den lägsta bithastighetsprofilen för Konservativ, den profil som ligger närmast mediandbithastigheten för tillgängliga profiler för Moderate och den högsta bithastighetsprofilen för Aggressiv.<br/><br/>Principen fungerar inom begränsningarna för lägsta och högsta bithastighet, om de anges.  Returnerar den aktuella inställningen från uppräkningen ABRControlParameters: <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>Se även [ABRPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* Felväxlingsmekanismen för TVSDK kan åsidosätta dessa inställningar eftersom TVSDK prioriterar en kontinuerlig uppspelning framför att strikt respektera kontrollparametrarna.
>* När bithastigheten ändras skickar TVSDK `onProfileChanged` händelser i `PlaybackEventListener`.


## Aktivera anpassad ABR-kontroll i referensimplementeringen {#section_72A6E7263E1441DD8D7E0690285515E6}

Adaptiv bithastighet (ABR) är aktiverat i TVSDK som standard. Du kan använda användargränssnittet Primetime Settings för att åsidosätta TVSDK-standardbeteendet i referensimplementeringen genom att konfigurera en anpassad ABR-kontroll.

Så här aktiverar du anpassad ABR via inställningsgränssnittet:

* Öppna dialogrutan Primetime-inställningar.
* Välj **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* Tryck på [!UICONTROL Enable ON] kontrollen så att den visas `OFF`.

Anger `PlaybackManager` bara ABR-parametrar om [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) returnerar true (ON). Om det returnerar false (OFF) `PlaybackManager` använder ABR-standardkontrollen så att den inledande, lägsta och högsta bithastigheten blir 0 och ABR-principen blir `ABR_MODERATE`.

## Konfigurera för låg bithastighet {#section_5451691CBBD24542AD54A474D222CD39}

För vissa låga bithastighetsuppspelningshastigheter växlar TVSDK som standard till direktuppspelningen med endast ljud och uppspelningen ser fryst ut. Du kan konfigurera spelaren så att den aldrig stöter på en situation där den växlar till enbart ljud.

* Implementera [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) -gränssnittet:

* Kontrollera att [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) är högre än bithastigheten för enbart ljud (högre än 64000).
* Kontrollera att [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) är aktiverad.