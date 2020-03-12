---
description: 'null'
seo-description: 'null'
seo-title: Konfigurera en domänserver
title: Konfigurera en domänserver
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Konfigurera en domänserver{#set-up-a-domain-server}

Så här konfigurerar du en domänserver på en befintlig licensserverinstallation:

1. Öppna [!DNL tomcat/lib] filen i [!DNL flashaccess-refimpl.properties] katalogen.
1. Under `Domain CA certificate` alternativet fyller du i certifikatutfärdarens domäncertifikat.

   Det här certifikatet används sedan för att ta emot domäntoken.
1. Fyll i `Domain CA credential` informationen under `Domain CA credential certificate (PFX)` alternativet.

   Det här certifikatet används sedan för att signera domäncertifikat och token.
1. Ange värdet för `DomainServerlURL`.

   Om det här värdet anges `NULL`kan domänautentiseringen lyckas. När du ansluter till domänen kan det dock uppstå ett anslutningsdomänfel.
