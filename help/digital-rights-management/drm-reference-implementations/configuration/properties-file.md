---
title: Licensserverns egenskapsfil
description: Licensserverns egenskapsfil
copied-description: true
exl-id: 07cd9866-c29b-476e-a63f-9c5272ccd678
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Licensserverns egenskapsfil{#license-server-properties-file}

Licensservern refererar till egenskaper som anges i [!DNL flashaccess-refimpl.properties] -fil. Du kan referera till den filen direkt för information om specifika värden och för användningsinformation om varje egenskap. Ett fullt funktionellt exempel finns i [!DNL resources] katalog för referensimplementeringen ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Autentiseringsuppgifter** - Egenskapsfilen innehåller inställningar för platsen för de autentiseringsuppgifter som Adobe utfärdar till dig. Du kan ange dessa autentiseringsuppgifter i en [!DNL .pfx] en fil med ett lösenord eller ange ett alias och lösenord för en referens som lagras på en HSM. Du måste åtminstone konfigurera egenskaperna som är relaterade till transportautentiseringsuppgifterna och licensserverns autentiseringsuppgifter. Ange platsen för dina autentiseringsfiler i förhållande till katalogen som du anger i dialogrutan `config.resourcesDirectory` -egenskap.

**Flash Media Rights Management Server** - `flashaccess-refimpl.properties` filen innehåller också flera egenskaper som är relaterade till paketeringsinnehåll. De här egenskaperna används bara för metadatakonverteringen för Flash Media Rights Management Server 1.x. När du har ändrat värdena i den här egenskapsfilen startar du om licensservern.
