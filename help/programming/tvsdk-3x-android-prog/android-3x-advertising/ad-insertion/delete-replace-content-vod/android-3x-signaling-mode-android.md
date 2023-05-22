---
description: Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.
title: Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer
exl-id: f42a2db5-642f-4944-87f6-2d7d902a2837
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Effekt vid infogning och borttagning av annonser i signeringsläge och metadatakombinationer {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Du kan markera, ta bort och ersätta tidsintervall i VOD-strömmar genom att använda olika kombinationer av annonssignaleringsläge och metadata. Olika kombinationer av signaleringsläge och metadata ger olika beteenden.

>[!TIP]
>
>När det finns en konflikt mellan tidsintervall och annonseringslägen ger TVSDK tidintervallprioritet.

Följande tabell innehåller information om signaleringsläget och metadatakombinationsbeteenden:

**Serveröversikt**

| **Lägg till metadata** | **Skapade lösare** | **`PlacementInformations`skapad** | **Resulterande beteende** |
|--- |--- |--- |--- |
|  | Ta bort | Ta bort | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Raderade intervall |
| Ta bort, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervall borttagna, annonser infogade |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annonser infogade |
| Ersätt, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervall som ersatts |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall, inga annonser infogade |

**Manifest Cues**

| Lägg till metadata | Skapade lösare | `PlacementInformations` skapad | Resulterande beteende |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Annonser infogade |
| Ta bort, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervall borttagna, annonser infogade |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall, inga annonser infogade |
| Ta bort | Ta bort | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Raderade intervall |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall |
| Ersätt, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervall som ersatts |

**Anpassat tidsintervall**

| Lägg till metadata | Skapade lösare | `PlacementInformations` skapad | Resulterande beteende |
|--- |--- |--- |--- |
| Ta bort | Ta bort | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Raderade intervall |
| Ta bort, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervall borttagna, inga annonser infogade |
| Auditude | Auditude | Ingen | Inga annonser har infogats |
| Ersätt, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervall ersatta med annonser |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall |
| Mark, Auditude | Anpassad annons, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall, inga annonser infogade |

**Inte inställd (standard)**

| Lägg till metadata | Skapade lösare | `PlacementInformations` skapad | Resulterande beteende |
|--- |--- |--- |--- |
| Ta bort | Ta bort | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Raderade intervall |
| Ta bort, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervall borttagna, annonser infogade |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annonser infogade |
| Ersätt, Auditude | Ta bort, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervall ersatta med annonser |
| Mark | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Markerade intervall |
