---
seo-title: Viktiga funktioner
title: Viktiga funktioner
uuid: b1bded0f-4e45-4ff8-a7ce-dac3d3ec0ab0
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Viktiga funktioner {#key-features}

Adobe Access har följande viktiga funktioner:

* **Stöd för HLS-strömning (kräver Adobe Primetime):** Använd Adobe Access DRM med HLS-innehåll som kan direktuppspelas på alla plattformar som stöds av Flash eller Adobe Primetime (till exempel Desktop, iOS och Android).
* **Inbyggt stöd för iOS-program (kräver Adobe Primetime):** Använd Adobe Access DRM för att skydda video i dina iOS-program.
* **Stöd för Android-program (kräver Adobe Primetime):** Använd Adobe Access DRM för att skydda video i dina Android-program.
* **Skyddad strömning på Xbox (kräver Adobe Primetime)**.
* **Fjärradministration av iOS-nycklar (kräver Adobe Primetime):** Stöd för att leverera iOS-fjärrnycklar via en multi-tenant-nyckelserver, som kallas Adobe Access Key Server.
* **Beständigt materialskydd:** Innehållet förblir skyddat genom hela distributionskedjan. När innehållet har paketerats förblir det alltid skyddat, och delar av det dekrypteras endast vid uppspelningen och i enlighet med användningsreglerna.
* Eftersom innehållet paketeras med användningsregler och licensinformation följer alltid skyddet med innehållet. Om olicensierade konsumenter försöker spela upp innehållet dirigeras de om av den princip som är inbäddad i innehållet så att de kan hämta en giltig licens för innehållet.
* **Säker uppspelning av skyddat innehåll: **Beprövade krypteringsscheman används för att skydda innehåll från obehörig uppspelning.
* **Flexibla användningsregler:** Användningsregler avgör hur konsumenter kan använda skyddat innehåll. De användningsregler som stöds av Adobe Access kan användas för flera olika affärsmodeller, inklusive betalning per vy, filmuthyrning, prenumerationer eller reklamfinansierade tjänster. Användningsreglerna anges i den policy som du bäddar in i innehållet under paketeringen, eller kan anges av licensservern under licensköpet.
* **Utdataskydd:** Kontroller för skydd av utdata kan användas för att utnyttja skyddssystem som HDCP, CGMS-A eller Rovi (tidigare Macrovision) ACP. Detta kan hjälpa till att skydda utdata från digitalt innehåll (till exempel HDMI, DVI och UDI) och analoga (till exempel S-Video och komponentvideo) utdata.

   Du kan ange alternativ för skydd av utdata i den profil som du skapar för ditt innehåll, vilket ger eller nekar åtkomst till innehåll baserat på en enhets funktioner för skydd av utdata. Du kan till exempel ange att utdataskydd inte krävs för visst innehåll, men kräver utdataskydd för Premium-videoinnehåll, vilket förhindrar att innehåll skapas i operativsystem som saknar den här funktionen.

   Dessa regler används konsekvent på alla plattformar, men för närvarande går det bara att på ett säkert sätt aktivera utdataskydd på Windows-plattformar.

* **Stöd för dynamisk strömning: **Använd den dynamiska strömningsfunktionen i Flash Media Server eller Adobe HTTP Dynamic Streaming för att skydda innehåll som kodats med flera bithastigheter. Dynamisk direktuppspelning använder en videoström som dynamiskt anpassar bithastigheten och uppspelningskvaliteten baserat på tillgänglig bandbredd, vilket ger en förbättrad användarupplevelse. Med Adobe Access kan du använda samma krypteringsnyckel och licens för innehåll i olika kodningar av samma resurs.
* **Offlinevisning:** Med Adobe AIR runtime-klienten kan kunderna hämta och lagra innehåll för senare visning, oavsett om datorn fortfarande är ansluten till Internet eller inte.
* **Identitetsbaserad licensiering:** Länkar behörigheter till användaridentiteter som kräver att konsumenterna autentiserar sig (anger ett användar-ID och lösenord) för att få tillgång till innehållet. Identitetsbaserad licensiering kräver att den part som utvecklar klientprogrammet implementerar användarautentisering som en del av arbetsflödet för licenshämtning.
* **Licenskedja:** Gör det möjligt för konsumenterna att förlänga livet på allt innehåll genom att förnya en enda rotlicens. En av de främsta användningsområdena för licenssammanfogning är prenumerationsbaserade affärsmodeller, där licenser till ett stort antal innehållsfiler kan förnyas i slutet av en prenumerationsperiod genom att helt enkelt förnya rotlicensen.

   Både rot- och lövlicenser är bundna till konsumentens dator. Lövlicensen innehåller CEK och en referens till rotlicensen. Rotlicensen kan utöka de rättigheter som ges i lövlicensen. En konsument kan till exempel ha en lövlicens för 50 innehållsdelar som upphör att gälla vid slutet av en viss prenumerationsperiod. Om konsumenten laddar ned en ny rotlicens med ett nytt förfallodatum kan alla 50 innehållsdelar spelas upp tills den uppdaterade licensen upphör att gälla.

   I Adobe Access 2.0 introducerades licenssammanlänkning där både löv- och rotlicenserna är bundna till en viss dator. I Adobe Access 3.0 introduceras en förbättrad form av licenssammanlänkning där ett löv är bundet till en rotlicens och endast rotlicensen är bunden till en viss dator eller domän. Läs *Förbättrad licenskedja* i *Använda Adobe Access SDK för att skydda innehåll*.

* **Nyckelrotation:** Vid normal paketering krypteras innehållet med ColdFusion Key (CEK) och klienten får en licens som innehåller CK för att kunna använda innehållet. När tangentrotation är aktiverad kan nyckeln som används för att kryptera innehållet ändras så att nyckeln bara används för att kryptera en del av innehållet. Läs *Nyckelrotation* i *Använda Adobe Access SDK för att skydda innehåll*.

* **Out-of-band-licenser:** Med Adobe Access är det möjligt att implementera ett arbetsflöde där klienter får förgenererade licenser utan att behöva installera en licensserver.
* **Domänstöd:** Som ett alternativ till att binda en licens till en viss enhet har Adobe Access stöd för att binda licenser till en domän. Flera enheter kan ansluta till en domän och få en domäntoken som tillåter att licenser flyttas mellan enheter i domänen. Läs *Domänregistrering* i *Använda Adobe Access SDK för att skydda innehåll*.

* **Partiell kryptering:** Anger om alla bildrutor, eller bara en delmängd av bildrutor, ska krypteras. Det finns tre krypteringsnivåer: låg, medel och hög. Om du minskar krypteringsnivån kan CPU-belastningen på datorer med lägre prestanda minska.
* **Paketering av innehåll som inte är anslutet:** Paketering av innehåll kräver ingen nätverksanslutning till licensservern. Detta möjliggör säkra backend-åtgärder genom att begränsa exponeringen av komprimerat innehåll som ännu inte är skyddat.
* **Kontroll över klockåterställning: **Adobe Access ger en säker och korrekt beräkning av tiden för att upptäcka klockåterställning på klientdatorn. Detta medför rättigheter som rör åtkomst till innehåll under en viss tid och förhindrar konsumenterna från att åsidosätta åtkomsträttigheter genom att ändra tiden på datorn.
* **Individualisering**: Tillåter bindning av innehåll till en viss dator.
* **Programvitlista:** Tillåter klientkörningen att säkerställa att skyddat innehåll endast spelas upp i ett godkänt SWF- eller AIR-program.
* **Återkallande av kompromissade klienter: **Komprometterad klientprogramvara kan återkallas. Om Flash Player- eller Adobe AIR-miljön bedöms vara komprometterad kan tjänsten nekas dessa klienter tills de uppgraderar till en nyare och säkrare version av klientprogramvaran.
* **Flera profiler för samma videofil: **Ett enstaka videomaterial kan ha flera profiler inbäddade under paketeringen. När en licens utfärdas kan licensservern bestämma vilken av reglerna som ska användas, vilket gör det möjligt för en innehållsdistributör att använda samma skyddade fil för olika affärsmodeller (t.ex. uthyrning och elektronisk försäljning).

