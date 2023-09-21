---
description: Adobe® Access™ är en avancerad lösning för hantering av digitala rättigheter och skydd av innehåll för högvärdigt audiovisuellt innehåll. Med verktyg som du skapar med Java API:er kan du skapa profiler, tillämpa profiler på filer som innehåller ljud- och videoinnehåll och kryptera dessa filer. Stegen på hög nivå för att utföra dessa uppgifter är följande
title: Ökning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Ökning {#overview}

Adobe® Access™ är en avancerad lösning för hantering av digitala rättigheter och skydd av innehåll för högvärdigt audiovisuellt innehåll. Med verktyg som du skapar med Java API:er kan du skapa profiler, tillämpa profiler på filer som innehåller ljud- och videoinnehåll och kryptera dessa filer. Stegen på hög nivå för att utföra dessa uppgifter är följande:

1. Använd Java-API:erna för att ange principegenskaper och krypteringsparametrar.
1. Skapa en profil som beskriver användningsrollerna för innehållet. (Se [Arbeta med policyer](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Du kan skapa valfritt antal profiler. De flesta användare skapar ett litet antal profiler och tillämpar dem på många filer.

1. Paketera en mediefil.

   I detta sammanhang *paketera en fil* innebär att kryptera den och tillämpa en profil på den. (Se [Paketera mediefiler](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implementera licensservern för att utfärda en licens till användaren.

Det krypterade innehållet är nu klart för distribution och klienten kan begära licensen från servern.

SDK innehåller ett Java-API för att utföra dessa åtgärder, och innehåller referensimplementeringar av licensservern samt kommandoradsverktyg som baseras på Java-API:erna. Mer information finns i *Använda referensimplementeringar för Adobe Access*.

## Nyheter i Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **Extern CEK**: Möjlighet att integrera ett CMS-system (Content Key Management System) i arbetsflödena för DRM-licenser och innehållspaket i stället för att kryptera CK-paketet och paketera det i innehållets metadata. Se [Extern CEK-översikt för Adobe Access DRM](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Returlicens (verifikation)**: Möjlighet för en klient att returnera (eller ta bort) en licens som har utfärdats till klienten.
* **Xbox Key Server**: Möjlighet att skydda innehåll som skickas till Xbox och Xbox 360. (En Adobe Primetime-klient krävs.)

## Anpassade användningsregler {#custom-usage-rules}

Anger anpassade användningsregler. Anpassade data kan inkluderas i licenser som utfärdas av licensservern. Tolkningen/hanteringen av dessa data är helt och hållet upp till implementeringen av klientprogrammet och licensservern.

Exempel på användningsfall: Gör det möjligt att utöka användningsreglerna genom att tillåta andra affärsregler att förmedlas säkert som en del av policyn och/eller innehållslicensen. Av säkerhetsskäl bör det här alternativet användas tillsammans med alternativen för AIR-programmet eller Flash Player SWF tillåtelselista, eftersom de här användningsreglerna används i anpassad klientprogramkod. Mer information finns i [Körnings- och programbegränsningar](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
