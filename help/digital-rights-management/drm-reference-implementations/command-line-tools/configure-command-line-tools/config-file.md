---
description: 'null'
seo-description: 'null'
seo-title: Om konfigurationsfiler för kommandoradsverktyg
title: Om konfigurationsfiler för kommandoradsverktyg
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Om konfigurationsfiler för kommandoradsverktyg{#about-command-line-tools-configuration-files}

Kommandoradsverktygen söker efter [!DNL flashaccesstools.properties] i den katalog där du kör verktygen. Du kan dock använda alternativet `-c` när du kör ett kommandoradsverktyg för att ange en annan plats för standardvärdet [!DNL flashaccesstools.properties]. Du kan också använda `-c` för att ange en annan konfigurationsfil.

Konfigurationsfilerna för kommandoradsverktygen använder formatet *Java-egenskapsfilen*, som följande regler gäller för:

* Escape-omvända snedstreck med ytterligare ett omvänt snedstreck.

   Om du till exempel vill ange filen [!DNL C:\credentials.pfx] på en Windows-dator måste du ange den som [!DNL C:\\credentials.pfx] eller `C:/credentials.pfx`. Om du vill ange en fil på en Windows-nätverksserver måste du ange `\\\\server\\folder\\filename.pfx`
* Ta endast med *Latin-1* tecken.

   Om du vill använda tecken som inte är-*Latin-1* måste du använda rätt Unicode-escape-sekvens. Du kan också använda verktyget [!DNL native2ascii] (ingår i Java) på dina konfigurationsfilsposter.
