---
description: 'null'
seo-description: 'null'
seo-title: Konfigurera en domänserver
title: Konfigurera en domänserver
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Konfigurera en domänserver{#set-up-a-domain-server}

Så här konfigurerar du en domänserver på en befintlig licensserverinstallation:

1. Öppna filen [!DNL flashaccess-refimpl.properties] i katalogen [!DNL tomcat/lib].
1. Fyll i certifikatutfärdarcertifikatet för domänen under alternativet `Domain CA certificate`.

   Det här certifikatet används sedan för att ta emot domäntoken.
1. Fyll i `Domain CA credential certificate (PFX)`-informationen under alternativet `Domain CA credential`.

   Det här certifikatet används sedan för att signera domäncertifikat och token.
1. Ange värdet för `DomainServerlURL`.

   Om värdet är `NULL` kan domänautentiseringen lyckas. När du ansluter till domänen kan det dock uppstå ett anslutningsdomänfel.
