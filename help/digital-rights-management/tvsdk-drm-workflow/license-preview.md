---
title: Förhandsgranskning av licens
description: Förhandsgranskning av licens
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Förhandsgranskning av licens {#license-preview}

Om det finns en fråga om en enhet kan använda och tillämpa en Primetime DRM-licens fullt ut eller inte, kan du använda funktionen Förhandsgranska licens. En förhandsvisningslicens matchar alla begränsningar som definierats i den slutliga licensen, men innehåller inte den CK (Content Encryption Key) som behövs för att dekryptera det skyddade innehållet. Den här funktionen är användbar för att avgöra om kunden faktiskt kan förbruka licensen innan innehållsdistributören bestämmer sig för att tillhandahålla en viss licens till klienten. En kund vill till exempel titta på HD-innehåll, men innehållsdistributören vill vara säker på att enheten kan identifiera och aktivera HDCP fullt ut. I den här situationen kan kunden ringa `DRMManager.loadPreviewVoucher()`. Om en `DRMStatusEvent` tas emot i stället för `DRMErrorEvent`, så bekräftas det att klienten till fullo kan tillämpa begränsningarna för utdataskydd i licensen och att innehållsdistributören fritt kan tillhandahålla den här typen av licens till klienten.

[iOS obtainPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android obtainPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
