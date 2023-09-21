---
title: Om konfigurationsfiler för kommandoradsverktyg
description: Om konfigurationsfiler för kommandoradsverktyg
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Om konfigurationsfiler för kommandoradsverktyg{#about-command-line-tools-configuration-files}

Kommandoradsverktygen letar efter [!DNL flashaccesstools.properties] i den katalog där du kör verktygen. Du kan dock använda `-c` när du kör ett kommandoradsverktyg för att ange en annan plats för standardinställningen [!DNL flashaccesstools.properties]. Du kan också använda `-c` för att ange en annan konfigurationsfil.

Konfigurationsfilerna för kommandoradsverktygen använder *Java-egenskapsfil* format, för vilket följande regler gäller:

* Escape-omvända snedstreck med ytterligare ett omvänt snedstreck.

  På en Windows-dator anger du [!DNL C:\credentials.pfx] måste du ange den som [!DNL C:\\credentials.pfx] eller `C:/credentials.pfx`. Om du vill ange en fil på en Windows-nätverksserver måste du ange `\\\\server\\folder\\filename.pfx`
* Inkludera endast *Latin-1* tecken.

  Använda ej *Latin-1* måste du använda rätt Unicode-escape-sekvens. Du kan också använda [!DNL native2ascii] -verktyget (ingår i Java) till dina konfigurationsfilsposter.
