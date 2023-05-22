---
title: Konfigurera en domänserver
description: Konfigurera en domänserver
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
