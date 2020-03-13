---
description: 'null'
seo-description: 'null'
seo-title: Om konfigurationsfiler för kommandoradsverktyg
title: Om konfigurationsfiler för kommandoradsverktyg
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155

---


# Om konfigurationsfiler för kommandoradsverktyg{#about-command-line-tools-configuration-files}

Kommandoradsverktygen söker efter [!DNL flashaccesstools.properties] i den katalog där du kör verktygen. Du kan dock använda alternativet när du kör ett kommandoradsverktyg för att ange en annan plats för standardinställningen `-c` [!DNL flashaccesstools.properties]. Du kan också använda `-c` för att ange en annan konfigurationsfil.

Konfigurationsfilerna för kommandoradsverktygen använder *Java-egenskapsfilformatet* , som följande regler gäller för:

* Escape-omvända snedstreck med ytterligare ett omvänt snedstreck.

   Om du till exempel vill ange [!DNL C:\credentials.pfx] filen på en Windows-dator måste du ange den som [!DNL C:\\credentials.pfx] eller `C:/credentials.pfx`. Om du vill ange en fil på en Windows-nätverksserver måste du ange `\\\\server\\folder\\filename.pfx`
* Inkludera endast *Latin-1* -tecken.

   Om du vill använda tecken som inte är *latinska-1* måste du använda rätt Unicode-escape-sekvens. Du kan också använda [!DNL native2ascii] verktyget (ingår i Java) för dina konfigurationsfilposter.
