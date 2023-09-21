---
title: HSM-inställningar
description: HSM-inställningar
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# HSM-inställningar {#hsm-preferences}

Inställningar på den här fliken behöver bara anges om **[!UICONTROL Enable HSM]** är markerad på fliken Packager. I följande tabell beskrivs dessa inställningar:

| Inställningar | Beskrivning |
|---|---|
| Sun PKCS#11 Konfigurationsfilnamn | Den fullständiga sökvägen till Sun PKCS#11-providerns konfigurationsfil. Mer information om innehållet i den här konfigurationsfilen finns i referenshandboken för Java PKCS#11 på Solens webbplats. |
| Partitionslösenord | Lösenordet för HSM-partitionen som anges i konfigurationsfilen PKCS#11. |
| Certifikatalias för licensserver | Alias för servercertifikat som utfärdas av Adobe och som lagras på HSM. Det här certifikatet används för att kryptera CEK under paketeringen. Ange detta i stället för *Licensservercertifikat* på fliken Packager. |
| Transportcertifikatalias för licensserver | Alias för servertransportcertifikat som utfärdas av Adobe som lagras på HSM. Det här certifikatet används för att säkra kommunikationen mellan klienten och licensservern. Ange detta i stället för *Transportcertifikat för licensserver* på fliken Packager. |
| Autentiseringsalias för Packager | Alias för Adobe-utfärdade paketerarautentiseringsuppgifter (certifikat och privat nyckel) som lagras på HSM. Detta används för att signera metadata under paketeringen. Ange detta i stället för *Packager Credential* på fliken Packager. |
| Autentiseringsalias för licensservern | Alias för Adobe-utfärdade licensserverautentiseringsuppgifter (certifikat och privat nyckel) som lagras på HSM. Den här autentiseringsuppgiften används för att signera principuppdateringslistor. Ange detta i stället för *Autentiseringsuppgifter för licensservern* på fliken Lista över principuppdateringar. (Detta alias är antagligen detsamma som *Certifikatalias för licensserver*.) |
