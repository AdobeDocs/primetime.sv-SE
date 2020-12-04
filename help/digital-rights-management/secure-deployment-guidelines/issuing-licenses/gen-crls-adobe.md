---
description: Du kan använda Adobe Primetime DRM för att skapa listor över återkallade certifikat som kompletterar den lista över återkallade certifikat som publiceras av Adobe.
seo-description: Du kan använda Adobe Primetime DRM för att skapa listor över återkallade certifikat som kompletterar den lista över återkallade certifikat som publiceras av Adobe.
seo-title: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
title: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Genererar listor över återkallade certifikat som kompletterar dem som publicerats av Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Du kan använda Adobe Primetime DRM för att skapa listor över återkallade certifikat som kompletterar den lista över återkallade certifikat som publiceras av Adobe.

Primetimes DRM SDK kontrollerar och verkställer Adobe CRL:er. Du kan dock inte tillåta ytterligare klientdatorer genom att skapa en CRL som återkallar ytterligare datorautentiseringsuppgifter genom att skicka CRL:en till Primetime DRM SDK. När du utfärdar en licens kontrollerar SDK Adobe CRL och din CRL.

Information om hur du skapar CRL:er finns i [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
