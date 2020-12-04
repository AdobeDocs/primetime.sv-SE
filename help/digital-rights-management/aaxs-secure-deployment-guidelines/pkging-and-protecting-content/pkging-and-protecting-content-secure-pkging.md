---
seo-title: Säker paketering av innehåll
title: Säker paketering av innehåll
uuid: a5e7cc17-353b-47d1-b89c-a2ba3c9faca1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Paketera innehåll {#securely-packaging-content} på ett säkert sätt

Konfigurationsfilen för kommandoradsverktyget Adobe Access Media Packager kräver en PKCS12-autentiseringsuppgift som används vid paketeringen.

I referensimplementeringskommandoradsverktygen lagras lösenordet för PKCS12-inloggningsfilen i filen flashaccess.properties i klartext. Därför bör du vara extra försiktig när du skyddar datorn som är värd för filen och se till att den är i en säker miljö. (Se [Fysisk säkerhet och åtkomst](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

Paketeraren använder även transportcertifikaten för licensservern och licensservern. Denna informations integritet och sekretess måste skyddas. Endast behöriga enheter bör tillåtas att använda paketeraren. Om någon av dina privata nycklar har komprometterats ska du omedelbart informera Adobe Systems Incorporated så att certifikatet kan återkallas.

>[!NOTE]
>
>Med API kan du använda samma nyckel för flera olika typer av innehåll. För att säkerställa högsta säkerhetsnivå rekommenderar vi att den här funktionen bara används för FMS-innehåll med flera bitars hastighet. Du bör inte använda samma nyckel för flera filer som representerar olika innehåll.

Paketerings-API:t för Adobe Access utfärdar varningar under vissa förhållanden. Du måste granska dessa varningar för att avgöra om filerna har krypterats. Varningsmeddelandena kan ange att principen har upphört att gälla, att en okänd tagg eller ett okänt spår inte kommer att krypteras, att filmfragment inte krypteras (och referenser i dessa fragment kan bli ogiltiga) och att metadata inte krypteras.

Om innehåll paketeras med en princip med felaktiga attribut bör profilen uppdateras och den uppdaterade profilen måste göras tillgänglig för licensservern via en principuppdateringslista eller någon annan metod för att leverera den uppdaterade profilen till servern. Vissa principattribut kan inte ändras efter att principen har skapats. Om attributen är felaktiga hämtar du tillbaka innehållet från distributionswebbplatserna, återkallar policyn så att inga framtida licenser kan beviljas och krypterar om innehållet.

När förpackningen är klar förstörs inte paketeringsnyckeln uttryckligen. Men den skräpsamlas. Paketnyckeln finns därför kvar i minnet under en tid. du måste skydda dig mot obehörig åtkomst till datorn och vidta åtgärder för att se till att du inte visar några filer, t.ex. kärndumpar, som kan avslöja informationen.
