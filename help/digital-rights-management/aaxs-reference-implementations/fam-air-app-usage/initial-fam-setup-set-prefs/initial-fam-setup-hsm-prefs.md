---
seo-title: HSM-inställningar
title: HSM-inställningar
uuid: 1b97d582-d4b6-48cd-9c24-2d13493571e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM-inställningar {#hsm-preferences}

Du behöver bara ange inställningar på den här fliken om du har markerat kryssrutan på fliken Packager **[!UICONTROL Enable HSM]** . I följande tabell beskrivs dessa inställningar:

| Inställningar | Beskrivning |
|---|---|
| Sun PKCS#11 Konfigurationsfilnamn | Den fullständiga sökvägen till Sun PKCS#11-providerns konfigurationsfil. Mer information om innehållet i den här konfigurationsfilen finns i referenshandboken för Java PKCS#11 på Solens webbplats. |
| Partitionslösenord | Lösenordet för HSM-partitionen som anges i konfigurationsfilen PKCS#11. |
| Certifikatalias för licensserver | Alias för Adobe-utfärdat licensservercertifikat som lagras på HSM. Det här certifikatet används för att kryptera CEK under paketeringen. Ange det här i stället för *licensservercertifikat* på fliken Packager. |
| Transportcertifikatalias för licensserver | Alias för Adobe-utfärdat servertransportcertifikat som lagras på HSM. Det här certifikatet används för att säkra kommunikationen mellan klienten och licensservern. Ange det här i stället för *Transportcertifikat* för licensserver på fliken Packager. |
| Autentiseringsalias för Packager | Alias för Adobe-utfärdade autentiseringsuppgifter för paketerare (certifikat och privat nyckel) lagrade på HSM. Detta används för att signera metadata under paketeringen. Ange detta i stället för *Packager Credential* på fliken Packager. |
| Autentiseringsalias för licensservern | Alias för autentiseringsuppgifter för Adobe-utfärdad licensserver (certifikat och privat nyckel) lagrade på HSM. Den här autentiseringsuppgiften används för att signera principuppdateringslistor. Ange detta i stället för *Autentiseringsuppgifter* för licensservern på fliken Lista för principuppdatering. (Detta alias är troligtvis detsamma som *licensserverns certifikatalias*.) |

