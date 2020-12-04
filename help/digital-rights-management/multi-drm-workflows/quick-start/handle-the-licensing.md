---
description: Licensiering är den primära mekanismen genom vilken användare tillåts eller nekas möjlighet att spela upp ett skyddat videoinnehåll. En berättigad (berättigad) användare kan få en licens (en nyckel) för att dekryptera och spela upp en viss del av innehållsleverantörens krypterade innehåll.
seo-description: Licensiering är den primära mekanismen genom vilken användare tillåts eller nekas möjlighet att spela upp ett skyddat videoinnehåll. En berättigad (berättigad) användare kan få en licens (en nyckel) för att dekryptera och spela upp en viss del av innehållsleverantörens krypterade innehåll.
seo-title: Licenser
title: Licenser
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# Licenser{#licensing}

Licensiering är den primära mekanismen genom vilken användare tillåts eller nekas möjlighet att spela upp ett skyddat videoinnehåll. En berättigad (berättigad) användare kan få en licens (en nyckel) för att dekryptera och spela upp en viss del av innehållsleverantörens krypterade innehåll.

Innan din app eller webbsida på en slutanvändares enhet kan spela upp DRM-skyddat innehåll måste den hämta en token från en berättigande- eller butiksserver som du, kunden, använder. Adobe tillhandahåller en exempelreferensserver för detta ändamål: [Referensserver: Exempel på ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

Din berättigande- eller butiksserver begär en licenstoken från den relevanta ExpressPlay-servern först efter att ha kontrollerat med dina egna bakomliggande system för att avgöra om den specifika användaren har rätt att titta på det begärda innehållet. Svaret som returneras från licenstokenbegäran är antingen en färdig URL för licensservern, eller så innehåller svaret URL:en i en JSON-struktur, beroende på vilken DRM-lösning du arbetar med.

>[!NOTE]
>
>Licenstokenbegäran kan inte göras från själva klienten:
>1. Rättigheterna ska kontrolleras i en tillförlitlig miljö. och
>1. Kundautentiseraren måste hemlighållas.


1. Gör en begäran om licenstoken.

   I ett snabbstartsscenario där du bara vill försäkra dig om att de olika komponenterna fungerar tillsammans, kanske du vill använda något som [!DNL curl] för att göra din licensförfrågan (till skillnad från att först få igång ett program och testa anrop därifrån). Exempel:

   * WideVM:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   Exempel på token för test av vinstockar:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   Observera att Widewin-svaret är en URL-sträng som är klar att användas.

   * PlayReady:

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   Exempel på testtoken för PlayReady:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   Observera att PlayReady-svaret är ett JSON-objekt med separata URL- och tokenelement.

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   Exempel på test-token för FairPlay:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   Observera att FairPlay-svaret är en URL-sträng som är klar att användas.
