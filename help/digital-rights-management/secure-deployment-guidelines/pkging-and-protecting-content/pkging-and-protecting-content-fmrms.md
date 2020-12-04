---
description: Flash Media Rights Management Server 1.x och Adobe Primetime DRM använder olika metadata för att paketera innehåll och begära licenser. För att Primetime DRM ska kunna använda FMRMS version 1.x-innehåll måste metadata konverteras.
seo-description: Flash Media Rights Management Server 1.x och Adobe Primetime DRM använder olika metadata för att paketera innehåll och begära licenser. För att Primetime DRM ska kunna använda FMRMS version 1.x-innehåll måste metadata konverteras.
seo-title: Säkerställer kompatibilitet med Flash Media Rights Management Server 1.x
title: Säkerställer kompatibilitet med Flash Media Rights Management Server 1.x
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Säkerställer kompatibilitet med Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x och Adobe Primetime DRM använder olika metadata för att paketera innehåll och begära licenser. För att Primetime DRM ska kunna använda FMRMS version 1.x-innehåll måste metadata konverteras.

Primetime DRM SDK har stöd för följande alternativ för konvertering av metadata:

* Offline (rekommenderas)

   Generera Primetimes DRM-metadata i en offlineprocess och lagra metadata tills klienten begär det. Om metadata genereras offline behöver licensservern inte åtkomst till 1.x-CEK:n eller paketerarens autentiseringsuppgifter. Konvertering offline ger bättre prestanda eftersom licensservern inte behöver generera metadata i realtid.
* On-demand

   Primetimes DRM-metadata genereras när metadata begärs av en klient. När en Primetime DRM-klient hämtar version 1.x-innehåll skickar klienten DRM-metadata till Primetimes DRM SDK. SDK konverterar DRM-metadata till det aktuella formatet, krypterar och bäddar in innehållskrypteringsnyckeln (CEK) i metadata och skickar tillbaka innehållet till Primetime DRM-klienten.

   >[!NOTE]
   >
   >Primetimes DRM 1.x-metadata innehåller inte CEK.

   För att kunna konvertera metadata måste Primetime DRM ha tillgång till innehållskrypteringsnycklarna Primetime DRM 1.x. När du migrerar från Flash Media Rights Management Server 1.x kan du fortsätta att lagra innehållskrypteringsnycklarna i LiveCycle ES-databasen eller implementera en anpassad lösning för att säkert lagra innehållskrypteringsnycklarna på en annan plats. Om du bestämmer dig för att lagra innehållskrypteringsnycklarna i LiveCycle ES-databasen följer du rekommendationerna som beskrivs i *Skydda åtkomst till känsligt innehåll i databasen* i **Förbättring och skydd för LiveCycle® ES2**.

Mer information om hur du säkerställer kompatibilitet med innehåll som paketerats med Flash Media Rights Management Server 1.x finns i Adobe Primetime DRM API:er på [Adobe Primetime API-referenser](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
