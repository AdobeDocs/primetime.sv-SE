---
seo-title: Komma igång
title: Komma igång
uuid: 2002cf94-c8a7-4820-a560-6d9f7f33ee97
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Komma igång {#getting-started}

I det här dokumentet beskrivs stegen för snabb installation och driftsättning av ett Adobe Primetime DRM-ekosystem som använder progressiv nedladdning för att distribuera innehåll, samt Primetime DRM-servern för skyddad direktuppspelning för licensdistribution. Ytterligare information om varje steg finns i följande handböcker:

* *Använda Primetime DRM-servern för att skydda innehåll*
* *Använda Primetime DRM-servern för skyddad strömning*

Primetimes DRM-server för skyddad direktuppspelning är en server med minimal funktionalitet som inte innehåller källkod. En ändringsbar server med fullständig Java-källa finns i guiden *Använda implementeringar* av Primetimes DRM-referens. Om du konfigurerar en referenslicensserver ersätter det steget *Konfigurera och distribuera Primetime DRM Server för skyddad direktuppspelning (licensserver)* .

## Förutsättningar {#prerequisites}

Utför följande uppgifter innan du börjar:

* Hämta två Windows- eller Linux-datorer:

   * En dator blir licensservern.
   * En dator blir Content Server.

* Installera följande program på båda datorerna:

   * Tomcat 6.0.18
   * Java 1.6

## Hämta certifikat {#obtain-certificates}

När SDK-programvaran har levererats får den utsedda företagscertifikatadministratören en inbjudan om att slutföra registreringsprocessen för DRM-certifikat för Adobe Primetime. Mer information finns i *Handboken* för registrering av DRM-certifikat för Primetime.

1. Administratören utser minst en person att fungera som certifikatbegärande.
1. Certifikatbegäraren genererar en privat nyckel och en CSR.
1. Begäranden skickar en certifikatbegäran.
1. Företagsadministratören godkänner begäran.
1. Adobe Certificate Administrator bekräftar inlämningen.
1. Begäraren tar emot certifikatet, binder certifikatet med den privata nyckeln och distribuerar certifikatet. enligt beskrivningen i .

   Mer information om hur du distribuerar certifikatet finns i guiden *Distribuera Adobe Primetime DRM Server for Protected Streaming* .
1. Steg 3 till 6 måste slutföras för varje certifikattyp.

   För Primetimes DRM-produktionsversion måste den begärande parten göra separata begäranden för licensservern, paketeringen och transportcertifikaten, som är giltiga i två år.

   Kunder som använder Primetime DRM Evaluation eller Trial behöver bara ett certifikat som är giltigt i 1 år respektive 90 dagar.