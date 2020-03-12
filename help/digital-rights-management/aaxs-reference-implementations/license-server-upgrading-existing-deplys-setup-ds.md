---
seo-title: Konfigurera en domänserver
title: Konfigurera en domänserver
uuid: b262ea86-f465-4ed1-b278-122d4dafc881
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Konfigurera en domänserver {#set-up-a-domain-server}

Så här konfigurerar du domänservern på en befintlig licensserverinstallation:

1. Öppna [!DNL flashaccess-refimpl.properties] filen under [!DNL tomcat/lib].

1. Fyll i certifikatinformationen för domäncertifikatutfärdare under `Domain CA certificate` alternativet. Det här certifikatet kommer att användas för att acceptera domäntoken.
1. Fyll i informationen under `Domain CA credential` alternativet `Domain CA credential certificate (PFX)` . Det här certifikatet kommer att användas för att signera domäncertifikat och tokens.

1. Ange värdet för `DomainServerlURL`. Om det här värdet är NULL kan domänautentiseringen lyckas. När du ansluter till domänen uppstår dock ett anslutningsdomänfel.

