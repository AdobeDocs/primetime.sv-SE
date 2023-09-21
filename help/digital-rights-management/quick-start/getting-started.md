---
title: Komma igång
description: Komma igång
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Komma igång {#getting-started}

Det här dokumentet innehåller stegen för att snabbt installera och driftsätta ett Adobe Primetime DRM-ekosystem som använder Progressiv nedladdning för att distribuera innehåll, samt Primetime DRM-servern för skyddad direktuppspelning för licensdistribution. Ytterligare information om varje steg finns i följande handböcker:

* *Använda Primetime DRM-servern för att skydda innehåll*
* *Använda Primetime DRM-servern för skyddad strömning*

Primetimes DRM-server för skyddad direktuppspelning är en server med minimal funktionalitet som inte innehåller källkod. En ändringsbar server med fullständig Java-källa finns i *Använda implementeringar av DRM-referenser för Primetime* guide. Om du konfigurerar en referenslicensserver ersätter det *Konfigurera och distribuera Primetime DRM Server for Protected Streaming (licensserver)* steg.

## Förutsättningar {#prerequisites}

Utför följande uppgifter innan du börjar:

* Hämta två Windows- eller Linux-datorer:

   * En dator blir licensservern.
   * En dator blir Content Server.

* Installera följande program på båda datorerna:

   * Tomcat 6.0.18
   * Java 1.6

## Hämta certifikat {#obtain-certificates}

När SDK-programvaran har levererats får den utsedda företagscertifikatadministratören en inbjudan om att slutföra registreringsprocessen för Adobe Primetime DRM-certifikat. Mer information finns i *Handbok för registrering av Primetime DRM-certifikat*.

1. Administratören utser minst en person att fungera som certifikatbegärande.
1. Certifikatbegäraren genererar en privat nyckel och en CSR.
1. Begäranden skickar en certifikatbegäran.
1. Företagsadministratören godkänner begäran.
1. Adobe certifikatadministratör bekräftar överföringen.
1. Begäraren tar emot certifikatet, binder certifikatet med den privata nyckeln och distribuerar certifikatet. enligt beskrivningen i .

   Mer information om hur du distribuerar certifikatet finns i *Driftsätta Adobe Primetime DRM Server for Protected Streaming* guide.
1. Steg 3 till 6 måste slutföras för varje certifikattyp.

   För Primetimes DRM-produktionsversion måste den begärande parten göra separata begäranden för licensservern, paketeringen och transportcertifikaten, som är giltiga i två år.

   Kunder som använder Primetime DRM Evaluation eller Trial behöver bara ett certifikat som är giltigt i 1 år respektive 90 dagar.
