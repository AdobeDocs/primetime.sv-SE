---
description: 'null'
seo-description: 'null'
seo-title: Lista över DRM-klienter som inte har åtkomst till skyddat innehåll
title: Lista över DRM-klienter som inte har åtkomst till skyddat innehåll
uuid: 38bc024e-0c5b-4c1c-8d4b-94b9e0fec67e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista över DRM-klienter som inte har åtkomst till skyddat innehåll {#blacklist-of-drm-clients-restricted-from-accessing-protected-content}

Den här svarta listan anger vilka DRM-klienter i Primetime som inte har åtkomst till skyddat innehåll. Ni svartlistar kunderna efter klientversion och plattform.

Exempel: Om en säkerhetslucka inträffar kan en nyare version av Primetime DRM-klienten anges som den minimiversion som krävs för hämtning av licenser och uppspelning av innehåll. Licensservern kontrollerar att Primetime DRM-klienten som gör licensbegäran uppfyller versionskraven innan licensen utfärdas. Primetimes DRM-klient kontrollerar även versionen i licensen innan innehållet spelas upp. Den här klientkontrollen krävs för domäner där en licens kan överföras till en annan dator.

En Primetime DRM-klientversion kan identifieras av de attribut som anges i följande tabell:

| **Attribut** | **Värden som stöds** | **Matcha villkor** | **Beskrivning** |
|---|---|---|---|
| Miljö | `“PC”, “PortingKit”` | Exakt matchning | Identifierar om klienten körs på en stationär dator eller någon annan enhet. |
| OS | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Exakt matchning | Plattform |
| Arkitektur | `“32”, “64”` | Exakt matchning | 32-bitars eller 64-bitars |
| Skärmtyp | `“PC”, “Mobile”, “TV”` | Exakt matchning |  |
| Körningsmiljöversioner | Ett giltigt versionsnummer. Till exempel `“2.0.0”, "3.0", "4.0", "11.0"`osv. | Matchar om klientversionen är mindre än eller lika med den angivna versionen. | Versionsnummer anges som en kombination av siffror och punkter (&quot;.&quot;) av valfri längd. |
| Primetime DRM Library-version | Ett giltigt versionsnummer. Till exempel `“2.0.0”`. | Matchar om klientversionen är mindre än eller lika med den angivna versionen. | Versionsnummer anges som en kombination av siffror och punkter (&quot;.&quot;) av valfri längd. |
| OEM-leverantör | OEM-leverantörssträng som kan hittas i det körningscertifikat som utfärdades till en kund som portade Primetime DRM till en enhet. | Exakt matchning | Identifieringssträng för OEM-leverantör för enheten med porteringsverktyget. |
| Modell | Modellsträng som kan hittas i körningscertifikatet som utfärdades till en kund som portade Primetime DRM till en enhet. Exempel: `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Exakt matchning | Identifieringssträng för enhetsmodell för enheten med porteringssatsen. |

>[!NOTE] {class=&quot;- topic/note &quot;
>
>När du anger en post i svartlistan kan du ange värden för ett eller flera av attributen som nämns i föregående tabell. Alla attribut som inte anges behandlas som jokertecken. Om Primetime DRM-klienten matchar alla värden som anges i en svartlistpost kanske klienten inte kommer åt skyddat innehåll.

