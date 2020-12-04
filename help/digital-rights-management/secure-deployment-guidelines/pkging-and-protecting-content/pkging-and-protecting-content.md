---
description: Information om paketering och skydd av innehåll gör att du kan skydda ditt innehåll.
seo-description: Information om paketering och skydd av innehåll gör att du kan skydda ditt innehåll.
seo-title: Paketera och skydda innehåll
title: Paketera och skydda innehåll
uuid: 9bf89f86-082e-40f9-8deb-c9774a9d8e02
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# Paketera och skydda innehåll {#packaging-protecting-content}

Information om paketering och skydd av innehåll gör att du kan skydda ditt innehåll.

## Skydda servern {#securing-the-server}

Ni måste fysiskt skydda den dator där policyer och innehållspaket används.

Mer information finns i [Fysisk säkerhet och åtkomst](../../secure-deployment-guidelines/physical-sec-and-access.md).

Om implementeringen av innehållspaketeringen kräver nätverksanslutning måste du skaffa ett extra operativsystem och implementera en lämplig brandväggslösning. Mer information finns i [Nätverkstopologi](../../secure-deployment-guidelines/overview/network-topology.md).

## Paketera innehåll {#securely-packaging-content} på ett säkert sätt

Konfigurationsfilen för kommandoradsverktyget Adobe Primetime DRM Media Packager kräver en PKCS12-autentiseringsuppgift som används vid paketeringen.

I verktygen för referensimplementering lagras lösenordet för PKCS12-inloggningsfilen i `flashaccess.properties`-filen i klartext. Därför bör du vara extra försiktig när du skyddar datorn som är värd för filen och ser till att datorn är i en säker miljö. Mer information finns i [Fysisk säkerhet och åtkomst](../../secure-deployment-guidelines/physical-sec-and-access.md).

Paketeraren använder även transportcertifikaten för licensservern och licensservern, och integriteten och sekretessen för informationen måste skyddas. Endast behöriga enheter bör tillåtas att använda paketeraren. Om dina privata nycklar har komprometterats ska du omedelbart informera Adobe Systems Incorporated så att certifikatet kan återkallas.

>[!NOTE]
>
>Med API kan du använda samma nyckel för flera olika typer av innehåll. För att säkerställa högsta säkerhetsnivå bör du bara använda den här funktionen för FMS-innehåll med flera bitars hastighet. Använd inte samma nyckel för flera filer som representerar olika innehåll.

Primetimes API för DRM-paketering utfärdar varningar under vissa förhållanden. Granska de här varningarna för att avgöra om filerna har krypterats. Varningsmeddelandena kan vara något av följande:

* Principen har upphört att gälla och en okänd tagg eller ett okänt spår kan inte krypteras.
* Filmfragment kan inte krypteras och referenser i dessa fragment kan vara ogiltiga.
* Det går inte att kryptera metadata.

Om innehåll paketeras med en princip med felaktiga attribut måste profilen uppdateras. Den uppdaterade profilen måste göras tillgänglig för licensservern via en principuppdateringslista eller någon annan leveransmekanism. Vissa principattribut kan inte ändras efter att principen har skapats. Om attributen är felaktiga hämtar du tillbaka innehållet från distributionswebbplatserna, återkallar policyn så att inga framtida licenser kan beviljas och krypterar innehållet igen.

När paketeringen är klar skräpsamlas paketeringsnyckeln och tas inte bort explicit. Därför finns paketeringsnyckeln kvar i minnet en tid. Du måste skydda dig mot obehörig åtkomst till datorn och se till att du inte visar några filer, t.ex. kärndumpar, som kan avslöja den här informationen.

## Säker lagring av profiler {#securely-storing-policies}

Med Adobe Primetime DRM SDK kan du utveckla program som kan användas för att paketera innehåll och skapa policyer.

När du skapar dessa program kan du tillåta vissa användare att skapa och ändra profiler och begränsa andra användare till att endast tillämpa befintliga profiler på innehållet. Du måste implementera nödvändiga åtkomstkontroller och skapa användarkonton med olika behörigheter för att skapa principer och principprogram.

Profiler signeras inte och skyddas inte från att ändras förrän de används i paketeringen. Om du är oroad över att användare av paketeringsverktyget kan ändra profiler, ska du signera profilerna för att säkerställa att profilerna inte kan ändras.

Mer information om hur du skapar program med SDK finns i Primetime DRM API:er i [API Primetime API-referenser](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Asymmetrisk nyckelkryptering {#asymmetric-key-encryption}

Asymmetrisk nyckelkryptering, som även kallas kryptering med offentlig nyckel, använder nyckelpar. Den ena nyckeln är för kryptering och den andra för dekryptering.

Dekrypteringsnyckeln, eller *`private key`*, hålls hemlig. krypteringsnyckeln, eller *`public key`*, är tillgänglig för alla som har behörighet att kryptera innehåll. Alla som har tillgång till den offentliga nyckeln kan kryptera innehållet. Det är dock bara någon som har tillgång till den privata nyckeln som kan dekryptera innehållet. Den privata nyckeln kan inte rekonstrueras från den offentliga nyckeln.

När du paketerar innehåll används licensserverns offentliga nyckel för att kryptera innehållskrypteringsnyckeln (CEK) i DRM-metadata. Du måste se till att bara licensservern har tillgång till licensserverns privata nyckel. Om någon annan har nyckeln kan de dekryptera och visa innehållet.

>[!CAUTION]
>
>Kontrollera att du har fått licensserverns certifikat som innehåller den offentliga nyckeln från en betrodd källa. På så sätt kan du se till att det är licensserverns nyckel och inte en obehörig offentlig nyckel. Om angriparna ersätter sin offentliga nyckel för licensserverns nyckel kan de dekryptera innehållet.

Mer information om hur du paketerar innehåll finns i [Använda Adobe Primetime DRM SDK för att skydda innehåll](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).