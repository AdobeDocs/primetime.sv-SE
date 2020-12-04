---
seo-title: Licensserver och bevakad mapppaketerare - översikt
title: Licensserver och bevakad mapppaketerare - översikt
uuid: 3dd6f699-a5c0-44c4-897a-34e06abe3d71
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Licensserver och bevakad mapppaketerare - översikt {#license-server-and-watched-folder-packager-overview}

Referensimplementeringsservern kan hjälpa dig att skapa en licensserver med hjälp av Adobe Access SDK. I den här implementeringen autentiseras användare baserat på användarposter i en databas. Servern innehåller affärslogik för att utfärda licenser. Det implementerar även kompatibilitetsstöd för Flash Media Rights Management Server 1.0 och 1.5.

Referensimplementeringsservern innehåller även en bevakad mappimplementering av paketeraren. Komponenten kan distribueras tillsammans med licensservern eller på en separat dator. Med den här paketeringsimplementeringen kan du skapa flera bevakade mappar. När innehåll släpps i den bevakade mappen paketeras innehållet automatiskt.

Licensservern och paketeraren distribueras som separata WAR-filer, så du kan välja om du vill köra dem på separata servrar eller i en enda Apache Tomcat®-instans. Licensservern finns i [!DNL flashaccess.war] och paketeraren är i [!DNL flashaccess-packager.war]. Det valfria [!DNL edcws.war] innehåller stöd för licensbegäranden från FMRMS 1.x-klienter.

Exemplskoden för referensimplementering visar följande funktioner:

* Licensserver:

   * Hantera autentiseringsbegäranden, använda en databas för att validera användarnamn/lösenord
   * Hantera licensförfrågningar och avgöra vilken typ av licens som ska utfärdas när licenskedjan används.
   * Utfärda licenser för innehåll som innehåller flera profiler
   * Utfärda licenser som stöder Remote Key-leverans till iOS-klienter (kräver Adobe Primetime)
   * Utfärdande av licenser som kräver en extern sökning/hämtning av innehållskrypteringsnyckeln (CEK)
   * Använd databasen för att avgöra om användaren har behörighet att visa innehåll
   * Använda listor för principuppdatering
   * Använda listor över datoråterkallade certifikat
   * Lagra autentiseringsuppgifter med en HSM- eller PKCS12-fil
   * Kryptera lösenord som anges i egenskapsfilen
   * Ange flera licensservrar eller transportreferenser (efter att inloggningsuppgifterna har förnyats sparas de gamla inloggningsuppgifterna på servern så att befintligt innehåll kan konsumeras utan att behöva paketeras om)
   * Begränsa DRM-/körningsversioner som tillåts göra förfrågningar till licensservern
   * Inställningar för klientens klockfönster
   * Begränsa tidsskillnaden mellan begärandetid och servertid (för att förhindra repetitionsattacker)
   * Hantera begäranden från FMRMS 1.x-klienter (utlöser en uppgradering till Adobe Access 2.0 eller senare från FMRMS 1.x-klienten)
   * Konvertera FMRMS 1.x-metadata till Adobe Access-metadata direkt med hjälp av FMRMS 1.x-licensinformation som lagras i en databas
   * Exempelkod för konvertering av FMRMS 1.x-principer till Adobe Access-principer
   * Exempelskript för import av FMRMS 1.x-licensinformation från en befintlig databas
   * Hämta serverversion
   * Domänregistrering
   * Avregistrering av domän
   * Synkroniseringsbegäranden
   * Licensretur

* Packager Server:

   * Implementera en paketeringsimplementering som automatiskt paketerar innehåll som lagts till i en bevakad mapp
   * Lagra autentiseringsuppgifter med en HSM- eller PKCS12-fil
   * Kryptera lösenord som anges i egenskapsfilen
   * Konfigurera paketeraren, skapa principer och skapa principuppdateringslistor med ett AIR-program

