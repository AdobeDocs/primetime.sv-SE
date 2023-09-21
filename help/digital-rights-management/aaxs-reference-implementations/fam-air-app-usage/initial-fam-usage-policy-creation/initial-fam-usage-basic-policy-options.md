---
title: Grundläggande principalternativ
description: Grundläggande principalternativ
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Grundläggande principalternativ {#basic-policy-options}

I följande tabell beskrivs de grundläggande principinställningarna:

| Inställningar | Beskrivning |
|---|---|
| Principvaraktighet | Anger giltighetsperioden för innehåll som skyddas med den här principen. |
|  | Börja vid | Licenser kan inte användas förrän detta datum/denna tid. |
|  | Sluta vid | Licenser kan inte användas efter detta datum/tid. |
|  | Sluta efter | Anger den tid en licens är giltig (i minuter), med början från den tidpunkt den paketeras. |
| Licenscache | Anger om licenser kan cachas av klienten. |
|  | | Licenser kan inte användas efter detta datum/tid. |
|  | Ta bort efter | Anger hur länge en licens är giltig (i minuter), med början från den tidpunkt då den utfärdas av licensservern. |
|  | Cachelagra oändligt | Licensen kan cachas på klienten på obestämd tid. |
|  | Ingen licenscache | Licensen får inte cachas av klienten. En ny licens måste hämtas från servern varje gång användaren spelar upp innehållet. |
| Autentisering | |
|  | Anonym | Ingen autentisering krävs för att visa innehållet. |
|  | Autentiserad | Autentisering av användarnamn/lösenord krävs. |
| Aktivera kedja av licenser | Tillåter att en licens uppdateras med en överordnad rotlicens för batchuppdatering av licenser. När lövlicensen upphör att gälla kan servern ge klienten en rotlicens som förnyar allt innehåll som skyddas med den här principen. |
