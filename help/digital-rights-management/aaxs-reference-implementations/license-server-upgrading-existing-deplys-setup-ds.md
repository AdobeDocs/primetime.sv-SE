---
title: Konfigurera en domänserver
description: Konfigurera en domänserver
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Konfigurera en domänserver {#set-up-a-domain-server}

Så här konfigurerar du domänservern på en befintlig licensserverinstallation:

1. Öppna [!DNL flashaccess-refimpl.properties] fil under [!DNL tomcat/lib].

1. Under `Domain CA certificate` fyller du i certifikatinformation för domän. Det här certifikatet kommer att användas för att acceptera domäntoken.
1. Under `Domain CA credential` alternativ, fyll i `Domain CA credential certificate (PFX)` information. Det här certifikatet kommer att användas för att signera domäncertifikat och tokens.

1. Ange värdet för `DomainServerlURL`. Om det här värdet är NULL kan domänautentiseringen lyckas. När du ansluter till domänen uppstår dock ett anslutningsdomänfel.
