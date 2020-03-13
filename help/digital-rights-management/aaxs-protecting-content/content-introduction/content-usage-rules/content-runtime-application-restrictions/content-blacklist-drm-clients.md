---
seo-title: Svartlista över DRM-klienter som inte har åtkomst till skyddat innehåll
title: Svartlista över DRM-klienter som inte har åtkomst till skyddat innehåll
uuid: c05aa6f8-32d9-42aa-a9c5-0d0629d49778
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Svartlista över DRM-klienter som inte har åtkomst till skyddat innehåll {#black-list-of-drm-clients-restricted-from-accessing-protected-content}

**DRM-modulversioner för Adobe Access är begränsade från åtkomst till skyddat innehåll.**

Anger den DRM-klient som inte har åtkomst till innehåll. Anges av DRM-klientversion och plattform.

Exempel: Vid säkerhetsöverträdelse kan en nyare version av DRM-klienten anges som den minimiversion som krävs för hämtning av licenser och uppspelning av innehåll. Licensservern kontrollerar att DRM-klienten som gör licensbegäran uppfyller versionskraven innan licensen utfärdas. DRM-klienten kontrollerar också DRM-versionen i licensen innan innehållet spelas upp. Den här klientkontrollen krävs för domäner där en licens kan överföras till en annan dator.

En DRM-klientversion kan identifieras av attributen som anges i följande tabell:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Miljö | &quot;PC&quot;, &quot;PortingKit&quot; | Exakt matchning | Identifierar om klienten körs på en stationär dator eller någon annan enhet. |
| OS | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Exakt matchning | Plattform |
| Arkitektur | “32”, “64” | Exakt matchning | 32-bitars eller 64-bitars |
| Skärmtyp | &quot;PC&quot;, &quot;Mobile&quot;, &quot;TV&quot; | Exakt matchning |  |
| Körningsmiljöversioner | Ett giltigt versionsnummer. Exempel: &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot; osv. | Matchar om klientversionen är mindre än eller lika med den angivna versionen. | Versionsnummer anges som en kombination av siffror och punkter (&quot;.&quot;) av valfri längd. |
| DRM-biblioteksversion | Ett giltigt versionsnummer. Till exempel &quot;2.0.0&quot;. | Matchar om klientversionen är mindre än eller lika med den angivna versionen. | Versionsnummer anges som en kombination av siffror och punkter (&quot;.&quot;) av valfri längd. |
| OEM-leverantör | OEM-leverantörssträng | Exakt matchning | Identifieringssträng för OEM-leverantör för enheten med porteringsverktyget. |
| Modell | Modellsträng. Exempel:&quot;iOS_Mobile&quot;,&quot;Android_Mobile&quot;,&quot;Chrome&quot;,&quot;ChromeOS_ARM&quot;,&quot;WindowsOnARM&quot;,&quot;AVE&quot; | Exakt matchning | Identifieringssträng för enhetsmodell för enheten med porteringssatsen. |

>[!NOTE] {class=&quot;- topic/note &quot;
>
>När du anger en post i svartlistan kan värden anges för ett eller flera av attributen som nämns i föregående tabell. Alla attribut som inte anges behandlas som jokertecken. Om DRM-klienten matchar alla värden som anges i en svartlistpost, kanske klienten inte kommer åt skyddat innehåll.

