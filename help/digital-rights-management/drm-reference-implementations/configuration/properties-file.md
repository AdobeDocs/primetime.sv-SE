---
title: Licensserverns egenskapsfil
description: Licensserverns egenskapsfil
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Licensserverns egenskapsfil{#license-server-properties-file}

Licensservern refererar till egenskaper som angetts i filen [!DNL flashaccess-refimpl.properties]. Du kan referera till den filen direkt för information om specifika värden och för användningsinformation om varje egenskap. Ett fullt funktionellt exempel finns i katalogen [!DNL resources] för referensimplementeringen ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Autentiseringsuppgifter**  - Egenskapsfilen innehåller inställningar för platsen för de autentiseringsuppgifter som Adobe utfärdar till dig. Du kan ange dessa autentiseringsuppgifter i en [!DNL .pfx]-fil med ett lösenord eller ange ett alias och lösenord för en autentiseringsuppgift som lagras på en HSM. Du måste åtminstone konfigurera egenskaperna som är relaterade till transportautentiseringsuppgifterna och licensserverns autentiseringsuppgifter. Ange platserna för dina autentiseringsfiler i förhållande till katalogen som du anger i egenskapen `config.resourcesDirectory`.

**Flash Media Rights Management Server**  -  `flashaccess-refimpl.properties` filen innehåller även flera egenskaper som är relaterade till paketeringsinnehåll. De här egenskaperna används bara för metadatakonverteringen för Flash Media Rights Management Server 1.x. När du har ändrat värdena i den här egenskapsfilen startar du om licensservern.
