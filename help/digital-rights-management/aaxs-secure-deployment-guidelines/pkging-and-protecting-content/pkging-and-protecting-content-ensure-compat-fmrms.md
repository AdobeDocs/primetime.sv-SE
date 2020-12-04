---
seo-title: Säkerställ kompatibiliteten med Flash Media Rights Management Server 1.x
title: Säkerställ kompatibiliteten med Flash Media Rights Management Server 1.x
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Säkerställ kompatibilitet med Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x och Adobe Access använder olika metadata för att paketera innehåll och begära licenser. För att Adobe Access ska kunna använda FMRMS version 1.x-innehåll måste metadata konverteras.

Adobe Access SDK har stöd för två alternativ för konvertering av metadata:

* Offline (rekommenderas)

   Generera Adobe Access-metadata i en offlineprocess och lagra dem för användning när en klient begär det. Adobe rekommenderar det här alternativet. Om metadata genereras offline behöver licensservern inte åtkomst till 1.x-CEK:n eller paketerarens autentiseringsuppgifter. Dessutom ger konvertering offline bättre prestanda eftersom licensservern inte behöver generera metadata i realtid.

* On-demand

   Generera Adobe Access-metadata on demand när en klient begär det. När en Adobe Access-klient hämtar version 1.x-innehåll skickas DRM-metadata (även kallat DRM-huvudet) till Adobe Access SDK. SDK konverterar DRM-metadata till det aktuella formatet. SDK krypterar och bäddar in innehållskrypteringsnyckeln (CEK) i metadata och skickar tillbaka innehållet till Adobe Access-klienten. (Adobe Access 1.x-metadata innehåller inte CEK.)

   Om du vill konvertera metadata måste du ha åtkomst till Adobe Access 1.x-innehållskrypteringsnycklarna för Adobe Access. När du migrerar från Flash Media Rights Management Server 1.x kan du fortsätta att lagra innehållskrypteringsnycklarna i LiveCycle ES-databasen eller implementera en anpassad lösning för att säkert lagra innehållskrypteringsnycklarna någon annanstans. Om du väljer att fortsätta lagra innehållskrypteringsnycklarna i LiveCycle ES-databasen följer du rekommendationerna i Skydda åtkomst till känsligt innehåll i databasen i *Förbättring och skydd för LiveCycle ES*.

Mer information om hur du säkerställer kompatibilitet med innehåll som paketerats med Flash Media Rights Management Server 1.x finns i *API-referens för Adobe Access*.
