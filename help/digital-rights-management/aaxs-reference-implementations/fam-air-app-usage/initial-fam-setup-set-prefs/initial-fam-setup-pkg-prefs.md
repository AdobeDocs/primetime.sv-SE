---
seo-title: Inställningar för Packager
title: Inställningar för Packager
uuid: 3e9c971d-3a5f-4f3e-97e7-baab63b1f67f
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Inställningar för Packager {#packager-preferences}

Fliken innehåller inställningar som krävs för att paketera innehåll. I följande tabell beskrivs dessa inställningar:

| Inställningar | Beskrivning |
|--- |--- |
| Transportcertifikat för licensserver | Servertransportcertifikatet, utfärdat av Adobe. Det här certifikatet används för att säkra kommunikationen mellan klienten och licensservern. Filen måste finnas i resurskatalogen. |
| Aktivera HSM | Anger om certifikat och autentiseringsuppgifter lagras på en HSM. I så fall inaktiveras inställningar för certifikat och autentiseringsuppgifter och egenskaperna på fliken NMI måste anges. |
| Alternativ för nyckelkryptering | Anger hur innehållskrypteringsnyckeln krypteras vid paketering |
| Licensservercertifikat | License Server-certifikatet som utfärdas av Adobe. Filen måste finnas i resurskatalogen. CEK krypteras med den offentliga nyckeln för licensservern. Endast innehavare av licensserverns privata nyckel får dekryptera CEK. |
| Packager Credential | Packager-autentiseringsuppgifterna som utfärdas av Adobe. Den här filen används för att signera metadata under paketeringen. |
| Filnamn | Filen `PKCS#12` (.pfx) som innehåller certifikat och privat nyckel. Filen måste finnas i resurskatalogen. |
| Fillösenord | Lösenord för pfx-fil |
| Egenskaper för global bevakad mapp | Anger inställningar som är gemensamma för alla bevakade mappar som har konfigurerats på den här servern. |
| Kontrollintervall i millisekunder | Anger hur ofta bevakade mappar ska söka efter nytt innehåll som ska paketeras. Servern itererar genom alla konfigurerade bevakade mappar och väljer sedan så här länge. |
| Namnsuffix för utdatafil | Anger ett filtillägg som ska läggas till i utdatafiler. Om till exempel .out anges och indatafilen är video.flv blir utdatafilen video.out.flv. |
| Säkerhetskopiera indatafiler | Anger om en kopia av det ursprungliga innehållet ska sparas. Om det här alternativet inte är markerat tas originalfilen bort när paketeringen har slutförts. |
| Namn på undermapp för säkerhetskopiering av indata | Om alternativet Säkerhetskopiera indatafiler är markerat anger en mapp där indatafilerna ska sparas. Det här alternativet anger ett mappnamn i förhållande till indatakatalogen för bevakade mappar. Om mappen inte finns skapas den under paketeringen. |
| Skriv över befintliga utdatafiler | Anger om utdatafilen kan skrivas över om det redan finns en fil med samma namn. Om det här alternativet inte är markerat och utdatafilen redan finns, hoppas bearbetningen av indatafilen över. |
