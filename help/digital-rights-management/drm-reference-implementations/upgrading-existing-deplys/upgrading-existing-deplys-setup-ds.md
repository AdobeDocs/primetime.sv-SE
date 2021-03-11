---
title: Konfigurera en domänserver
description: Konfigurera en domänserver
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
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
