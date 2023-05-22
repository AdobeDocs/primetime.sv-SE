---
title: Konfigurera en domänserver
description: Konfigurera en domänserver
copied-description: true
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Konfigurera en domänserver{#set-up-a-domain-server}

Så här konfigurerar du en domänserver på en befintlig licensserverinstallation:

1. I [!DNL tomcat/lib] katalog, öppna [!DNL flashaccess-refimpl.properties] -fil.
1. Under `Domain CA certificate` fyller du i certifikatutfärdarens domäncertifikat.

   Det här certifikatet används sedan för att ta emot domäntoken.
1. Under `Domain CA credential` , slutför `Domain CA credential certificate (PFX)` information.

   Det här certifikatet används sedan för att signera domäncertifikat och token.
1. Ange värdet för `DomainServerlURL`.

   Om värdet är inställt på `NULL`kan domänautentiseringen lyckas. När du ansluter till domänen kan det dock uppstå ett anslutningsdomänfel.
