---
description: Du kan använda Adobe Primetime DRM för att skapa listor över återkallade certifikat som kompletterar den lista över återkallade certifikat som publiceras av Adobe.
title: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Genererar listor över återkallade certifikat som kompletterar dem som publicerats av Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Du kan använda Adobe Primetime DRM för att skapa listor över återkallade certifikat som kompletterar den lista över återkallade certifikat som publiceras av Adobe.

Primetimes DRM SDK kontrollerar och verkställer Adobe CRL:er. Du kan dock inte tillåta ytterligare klientdatorer genom att skapa en CRL som återkallar ytterligare datorautentiseringsuppgifter genom att skicka CRL:en till Primetime DRM SDK. När du utfärdar en licens kontrollerar SDK Adobe CRL och din CRL.

Information om hur du skapar CRL:er finns i [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
