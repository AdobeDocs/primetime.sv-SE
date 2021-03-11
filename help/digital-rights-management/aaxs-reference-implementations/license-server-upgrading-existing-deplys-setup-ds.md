---
title: Konfigurera en domänserver
description: Konfigurera en domänserver
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Konfigurera en domänserver {#set-up-a-domain-server}

Så här konfigurerar du domänservern på en befintlig licensserverinstallation:

1. Öppna filen [!DNL flashaccess-refimpl.properties] under [!DNL tomcat/lib].

1. Fyll i certifikatinformationen för domäncertifikatutfärdaren under alternativet `Domain CA certificate`. Det här certifikatet kommer att användas för att acceptera domäntoken.
1. Fyll i `Domain CA credential certificate (PFX)`-informationen under alternativet `Domain CA credential`. Det här certifikatet kommer att användas för att signera domäncertifikat och tokens.

1. Ange värdet för `DomainServerlURL`. Om det här värdet är NULL kan domänautentiseringen lyckas. När du ansluter till domänen uppstår dock ett anslutningsdomänfel.

