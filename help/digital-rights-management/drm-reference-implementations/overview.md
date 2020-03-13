---
description: 'null'
seo-description: 'null'
seo-title: Referensimplementeringar
title: Referensimplementeringar
uuid: f08fdb4b-aaa8-4871-bb62-1a21d5abdd8d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Referensimplementeringar{#about-the-reference-implementations}

Den här guiden beskriver installation, konfiguration och drift av DRM-referensimplementeringar för Adobe Primetime.

>[!NOTE]
>
>Primetime DRM kallades tidigare för Adobe Access och tidigare för Flash Access.

Primetimes DRM-referensimplementeringar innehåller följande komponenter:

* **Kommandoradsverktyg** - Dessa verktyg är baserade på samma DRM SDK-kod för Primetime som används i DRM-licensservern för Primetime. Du kan paketera, licensiera och utföra andra DRM-åtgärder från kommandoraden och växla smidigt mellan kommandoradsverktygen och licensservern.
* **Licensserver** - En fullt fungerande, anpassningsbar licensserver (beskrivs nedan som ett av licensserveralternativen).

**Licensserveralternativ:**

* **Primetimes DRM-referensimplementeringar** - Den här referensimplementeringen är föremålet för den här guiden och innehåller en robust DRM-licensserver som visar alla funktioner som tillhandahålls av Primetime DRM SDK. Implementeringen levereras med källkod och instruktioner för hur du skapar koden. Den här implementeringen är inte avsedd att användas som den är (även om en [!DNL .war] fil ingår som du snabbt kan distribuera). Den är främst avsedd som referens som du kan använda för att skapa en egen anpassad licensserver.

   Licensserverfunktioner:

   * Hanterar autentiseringsbegäranden genom att använda en databas för att validera användarnamn/lösenord.
   * Hanterar licensförfrågningar och avgör vilken typ av licens som utfärdas när licenskedjan tillämpas.
   * Utfärdar licenser för innehåll som innehåller flera Primetime DRM-principer.
   * Utfärdar licenser som stöder Remote Key-leverans till iOS-klienter, vilket kräver Primetime DRM.
   * Utfärdar licenser som kräver en extern sökning och hämtning av innehållskrypteringsnyckeln (CEK).
   * Söker i en databas för att avgöra om en användare har behörighet att visa innehåll.
   * Söker i uppdateringslistor för DRM-principen Primetime.
   * Söker igenom listan över datoråterkallade certifikat.
   * Använder en HSM- eller PKCS12-fil för att lagra autentiseringsuppgifter.
   * Krypterar lösenord som du har angett i en egenskapsfil.
   * Anger flera licensservrar eller transportreferenser när autentiseringsuppgifterna har förnyats.

      De gamla inloggningsuppgifterna bevaras på servern så att användarna kan fortsätta att visa befintligt innehåll utan att behöva paketera om det.
   * Begränsar DRM-/körningsversioner som tillåts göra förfrågningar till en licensserver.
   * Anger inställningar för klientens klockfönster.
   * Begränsar tidsskillnaden som tillåts mellan begärandetiden och servertiden för att förhindra repetitionsattacker.
   * Hanterar begäranden från FMRMS 1.x-klienter

      Till exempel aktiveras klienten FMRMS 1.x för att uppgradera till Primetime DRM 2.0 eller senare.
   * Konverterar FMRMS 1.x-metadata till Primetime DRM-metadata vid behov genom att använda FMRMS 1.x-licensinformation som lagras i en databas.
   * Konverterar FMRMS 1.x-principer till Primetime DRM-principer för exempelkod.
   * Importerar FMRMS 1.x-licensinformation från en befintlig databas för exempelskript.
   * Hämtar serverversionen
   * Domänregistrering
   * Avregistrering av domän
   * Synkroniseringsbegäranden
   * Licensretur

* **Primetimes DRM-server för skyddad strömning** - Detta är en färdig binärfil som du kan implementera snabbt med minimal insats. Det är ett bra alternativ för kunder som snabbt vill visa konceptbevis, eller så *kan* det vara ett produktionsalternativ om dina anpassade DRM-behov är minimala. Mer information finns i Relaterad information nedan.

* **DRM-tjänsten** i Primetime Cloud - Det här är en licensserver från Adobe som du kan använda för licensanvändning. (Du måste vara en Primetime-licensinnehavare för att kunna använda den här tjänsten.) Denna molntjänst från Adobe befriar dig från kostnader, underhåll och teknik som krävs för att bygga din egen tjänst. Mer information finns i Relaterad information nedan.

