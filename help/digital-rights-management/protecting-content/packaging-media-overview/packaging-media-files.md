---
seo-title: Paketera mediefiler - översikt
title: Paketera mediefiler - översikt
uuid: 9509bcdc-ee4d-4025-9bb6-9b8ac439b926
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Översikt {#packaging-media-files-overview}

Paketering avser processen att kryptera och tillämpa en DRM-princip på videoinnehåll. Du kan använda API:erna för mediepaketering för att paketera filer. Primetime DRM Java SDK kan bara paketera innehåll för progressiv nedladdning, till exempel MP4.

>[!NOTE]
>
>Kontakta din DRM-representant på Primetime om hur du väljer det lämpligaste paketeringsalternativet för ditt medieformat och användningsexempel.

Paketeringen kopplas bort från licensservern. Paketeraren behöver inte ansluta till licensservern för att kunna utbyta information om innehållet. Allt licensservern behöver veta för att kunna utfärda en licens ingår i innehållets metadata.

När en fil är krypterad kan dess innehåll inte tolkas utan rätt licens. Du kan använda Primetime DRM för att markera de delar av filen som du vill kryptera. Eftersom Primetime DRM kan tolka videoinnehållets filformat kan det kryptera selektiva delar av en fil på ett intelligent sätt i stället för en hel fil. Data, som metadata och referenspunkter, kan förbli okrypterade så att sökmotorer fortfarande kan söka i filen.

Ett visst innehåll kan ha flera DRM-principer. Du kan till exempel licensiera innehåll under olika affärsmodeller utan att behöva paketera innehållet flera gånger. Dessutom kan ni tillåta anonym åtkomst under en kort period och sedan tillåta kunden att köpa innehållet för obegränsad åtkomst. Om innehåll paketeras med flera DRM-principer måste licensservern implementera logik för att välja vilken DRM-princip som ska användas för att utfärda en licens.

>[!NOTE]
>
>Med arkitekturen kan DRM-principer för användning anges och bindas till innehåll när innehållet paketeras. Innan en klient kan spela upp innehåll måste klienten hämta en licens för en angiven dator. Licensen anger vilka användningsregler som används och ger den nyckel som måste användas för att dekryptera innehållet. DRM-principen representerar en mall för att generera en licens. Licensservern kan dock åsidosätta användningsreglerna när den utfärdar en licens. Licensen kan vara ogiltig på grund av sådana begränsningar, t.ex. förfallotider eller uppspelningsfönster.

Primetime DRM tillhandahåller ett API för att skicka CEK. Om inget CEK anges genereras det slumpmässigt av SDK. Vanligtvis behöver du olika CEK-värden för varje innehållsavsnitt. I Dynamic Streaming är det emellertid troligt att du använder samma CEK för alla filer som innehåller det innehållet. Därför behöver en användare bara en licens för att smidigt kunna gå över från en bithastighet till en annan. Om du vill använda samma nyckel och licens för flera innehållsdelar måste du skicka samma `DRMParameters` objekt till `MediaEncrypter.encryptContent()`eller skicka in CEK med `V2KeyParameters.setContentEncryptionKey()`. Om du vill använda en annan nyckel och licens för varje innehållsavsnitt måste du skapa en ny `DRMParameters` instans för varje fil.

När du paketerar innehåll med tangentrotation kan du styra de rotationstangenter som används och med vilken frekvens tangenterna ska ändras. `F4VDRMParameters` och `FLVDRMParameters` implementera `KeyRotationParameters` gränssnittet. I det här gränssnittet kan du aktivera tangentrotation. Du måste också ange en `RotatingContentEncryptionKeyProvider`. För varje krypterat exempel avgör den här klassen vilken rotationsnyckel som ska användas. Du kan implementera en egen leverantör eller använda den `TimeBasedKeyProvider` som ingår i SDK:n. Implementeringen genererar slumpmässigt en ny nyckel efter ett angivet antal sekunder.

I vissa fall kan du behöva lagra innehållets metadata som en separat fil och göra den tillgänglig för klienten separat från innehållet. I så fall måste du anropa `MediaEncrypter.encryptContent()`, vilket returnerar ett `MediaEncrypterResult` objekt. Anropa `MediaEncrypterResult.getKeyInfo()` och omvandla resultatet till `V2KeyStatus`. Hämta sedan innehållets metadata och lagra dem i en fil.

Alla dessa åtgärder kan utföras med Java API.

Mer information om Java API finns i *Adobe Primetime DRM API Reference* .

Mer information om referensimplementeringen av Media Packager finns i *Använda referensimplementeringar* för Adobe Primetime DRM.
