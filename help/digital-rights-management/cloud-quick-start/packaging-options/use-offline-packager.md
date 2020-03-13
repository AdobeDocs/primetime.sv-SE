---
seo-title: Använd den medföljande offline-paketeraren i Primetime
title: Använd den medföljande offline-paketeraren i Primetime
uuid: 16b535a9-81b5-43bc-9e42-a64eb6649d9a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Använd den medföljande offline-paketeraren i Primetime{#use-the-included-primetime-offline-packager}

Din Primetime Java Packager levereras förkonfigurerad med de flesta inställningar du behöver för att paketera innehåll. Det finns bara ett fåtal områden att uppdatera för att komma igång.

## Uppdatera paketeringsegenskaper {#section_99904D35E99944A28FF43D924E516CC2}

Kontext för aktuell uppgift

* Uppdatera följande paketeringsegenskaper innan du använder konfigurationsfilen för att paketera innehållet:

### Egenskaper för XML-konfigurationsfil som tillhandahålls av användaren

| Egenskapsnamn | Beskrivning |
|---|---|
| `policy_file` | principfilens sökväg. Adobe ska tillhandahålla flera förkonfigurerade profiler att välja bland. |
| `pkgr_pfx` | Sökväg till Packager-autentiseringsuppgifter. Du måste ange dina egna Adobe-utgivna autentiseringsuppgifter ( [!DNL .pfx]) här. |
| `pkgr_pfx_pwd` | Lösenord för Packager-autentiseringsuppgifter. Du måste ange lösenordet till din Adobe-utgivna paketeringsautentisering här. |

## Paketera med kommandorad {#section_DFBE462679E34D62963BE201FD3321F9}

Kontrollera att du har fått all nödvändig information i konfigurationsfilen innan du paketerar innehåll.

* Använd följande syntax på kommandoraden för att paketera innehåll med konfigurationsfilen:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Exempelkonfigurationsfiler som paketerar ditt innehåll till HLS- eller HDS-format tillhandahålls, namngivna [!DNL config_hds.xml] och [!DNL config.hls.xml].

HDS- eller HLS-innehållet kommer att skrivas ut i mappen [!DNL /output] under katalogen Protection Kit. Alla artefakter som skrivs till den här katalogen måste finnas på en HTTP-webbserver för att kunna spelas upp.
