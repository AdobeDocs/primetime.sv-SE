---
title: Använd den medföljande offline-paketeraren i Primetime
description: Använd den medföljande offline-paketeraren i Primetime
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Använd den medföljande offline-paketeraren i Primetime{#use-the-included-primetime-offline-packager}

Din Primetime Java Packager levereras förkonfigurerad med de flesta inställningar du behöver för att paketera innehåll. Det finns bara ett fåtal områden att uppdatera för att komma igång.

## Uppdatera paketeringsegenskaper {#section_99904D35E99944A28FF43D924E516CC2}

Kontext för aktuell uppgift

* Uppdatera följande paketeringsegenskaper innan du använder konfigurationsfilen för att paketera innehållet:

### Egenskaper för XML-konfigurationsfil som tillhandahålls av användaren

| Egenskapsnamn | Beskrivning |
|---|---|
| `policy_file` | principfilens sökväg. Adobe ska tillhandahålla flera förkonfigurerade strategier att välja bland. |
| `pkgr_pfx` | Sökväg till Packager-autentiseringsuppgifter. Du måste ange egna Adobe-utfärdade autentiseringsuppgifter för paketeraren ( [!DNL .pfx]) här. |
| `pkgr_pfx_pwd` | Lösenord för Packager-autentiseringsuppgifter. Du måste ange lösenordet till din Adobe-utgivna paketerarautentiseringsuppgift här. |

## Paketera med kommandorad {#section_DFBE462679E34D62963BE201FD3321F9}

Kontrollera att du har fått all nödvändig information i konfigurationsfilen innan du paketerar innehåll.

* Använd följande syntax på kommandoraden för att paketera innehåll med konfigurationsfilen:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Exempelkonfigurationsfiler för att paketera ditt innehåll till HLS- eller HDS-format tillhandahålls, med namnet [!DNL config_hds.xml] och [!DNL config.hls.xml].

HDS- eller HLS-innehållet skickas till [!DNL /output] i mappen Protection Kit. Alla artefakter som skrivs till den här katalogen måste finnas på en HTTP-webbserver för att kunna spelas upp.
