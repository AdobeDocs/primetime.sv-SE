---
title: Amazon FireOS SSO med Clientless API Cookbook
description: Amazon FireOS SSO med Clientless API Cookbook
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Amazon FireOS SSO med Clientless API Cookbook {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>

## Introduktion {#Introduction}

Det här dokumentet innehåller anvisningar om hur du implementerar Amazon SSO-versionen av Adobe Primetime Authentication-flödet med klientlöst API. Den första delen av detta dokument fokuserar på detaljerna i Amazon-versionen av arkitekturen för de många partners som redan är bekanta med och har erfarenhet av att implementera den.

Den andra delen av dokumentet går igenom huvudstegen för att implementera klientlöst API för Adobe Primetime Authentication.

En utförlig teknisk översikt över hur den klientlösa lösningen fungerar finns i [REST API - översikt](/help/authentication/rest-api-overview.md). Adobe är den kontaktperson som föredrar att få support för den övergripande arkitekturen och de första implementeringarna.

## Amazon klientlös SSO {#AMZ-Clientless-SSO}

### Arkitektur på hög nivå {#High-Level-Arch}

Amazon klientlösa SSO-implementering är enkel och i huvudsak identisk med vanliga Adobe Primetime Authentication-klientlösa API:er.

Du måste använda Amazon SDK för att hämta en anpassad nyttolast och använda den när du anropar klientlösa API:er för Adobe.

Om nyttolasten känns igen och motsvarar en autentiserad session, kommer de klientlösa API:erna att returneras direkt med sessionens token.

### Så här skapar du programmet som ska använda Amazon SDK {#Build-entries}

* Hämta och kopiera den senaste [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) till en /SSOEnabler-mapp som är parallell med programkatalogen
* Uppdatera manifest-/gradle-filer så att biblioteket används:

  **Lägg till följande rad i din Manifest-fil:**

  ```Java
  <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
  ```

  **Poster i övertoningsfil:**

  Under databaser:

  ```java
  flatDir {
       dirs '../SSOEnabler'
  }
  ```

  Lägg till under beroenden:

  ```Java
  provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
  ```


* Hantera frånvaron av Amazon app:

  Även om det inte är troligt att följeslagaren inte finns på den Amazon-enhet som programmet körs på, bör du stöta på ett ClassNotFoundException vid körning för följande klass: `com.amazon.ottssotokenlib.SSOEnabler`.

  Om detta skulle inträffa behöver du bara hoppa över nyttolaststeget och återgå till det vanliga PrimeTime-flödet. SSO kommer inte att aktiveras, men ett vanligt autentiseringsflöde sker normalt.

</br>

### Så här får du Amazon SSO-nyttolast med Amazon SDK {#UseAmazonSSO}

Hämta en instans av SSOEnabler när programmet initieras. Baserat på din programarkitektur bör du välja mellan en synkron eller asynkron implementering.

Om API-anropen av någon anledning inte returnerar någon nyttolast använder du det vanliga icke-SSO-flödet och kontaktar Amazon och Adobe partners för att undersöka detta.

**Asynkront API**

* Hämta SSO-aktiveringsinstans:

  ```Java
  ssoEnabler = SSOEnabler.getInstance(context);
  SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
  ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
  ```


* Ange återanrop

  ```java
  public static abstract class SSOEnablerCallback
  {
          public abstract void getSSOTokenSuccess(Bundle result);
          public abstract void getSSOTokenFailure(Bundle result);
  }
  ```

   * Svarspaketet innehåller:
      * SSO-token som en sträng med nyckeln SSOToken
   * Svarspaket för fel kommer att innehålla:
      * felkod som int med nyckeln ErrorCode
      * felbeskrivning som en sträng med nyckeln &quot;ErrorDescription&quot;


* Hämta SSO-token

  ```JAVA
  Bundle getSSOTokenAsync(Void);
  ```

* Detta API ger svar via callback-funktionen som ställs in under initieringen.

  **Ex**. anrop med singleton-instans som skapats under init:

  ```JAVA
  ssoEnabler.getSSOTokenAsync().
  ```


**Synkrona API:er**

* Hämta instansen av SSO-aktivering och ange återanropet

  ```JAVA
  ssoEnabler = SSOEnabler.getInstance(context);</span>
  ```

* Hämta SSO-token

  ```JAVA
  Bundle getSSOTokenSync(Void);
  ```

   * Detta API blockerar anropartråden och svarar med resultatpaketet. Eftersom detta är ett synkront anrop bör du inte använda det i huvudtråden.

  ```JAVA
  void setSSOTokenTimeout(long);
  ```

   * Värde i millisekunder. om detta anges åsidosätter du standardvärdet för timeout på 1 minut för synk-API.


### Adobe Primetime Client-less API-uppdatering för dynamisk klientregistrering {#clientlessdcr}

Om detta är din första implementering, se **Kundfri teknisk översikt** och kontakta Adobe om du behöver hjälp.

Adobe klientlöst API kräver att program använder dynamisk klientregistrering för att anropa Adobe-servrar.

* Följ instruktionerna i om du vill använda dynamisk klientregistrering i ditt program [Registrering av programmet med dynamisk klientregistrering](/help/authentication/dynamic-client-registration-management.md).

* Följ instruktionerna i om du vill implementera API för registrering av dynamiska klienter för att utföra autentiserings- och auktoriseringsbegäranden till Adobe Primetime-servrar [API för dynamisk klientregistrering](/help/authentication/dynamic-client-registration-api.md) .

### API-uppdatering utan Adobe Primetime Client som använder Amazon SSO {#clientlesssso}

Amazon SSO-nyttolast som hämtas från Amazon SDK måste finnas på begäranden som görs till slutpunkterna för Adobe Primetime-autentisering:

```
      /adobe-services/*
      /reggie/*
      /api/*
```


Alla Primetime Authentication-slutpunkter har stöd för följande metoder för att ta emot identifieraren för Device-scope eller Platform-scope (finns i Amazon SSO-nyttolast):

* Som rubrik :&quot;Adobe-Subject-Token&quot;
* Som en frågeparameter: &quot;ast&quot;
* Som en post-parameter: &quot;ast&quot;


>[!NOTE]
>
>Om enhetsomfångets identifierare eller plattformsomfångets identifierare skickas som fråga/post-parameter måste den inkluderas när signaturen för begäran genereras.

>[!NOTE]
>
>Om frågeparametern&quot;ast&quot; används kan hela URL:en bli mycket lång och avvisas. Vid /authenticate-anrop kan den här parametern hoppas över eftersom den angavs vid /regcode-anropet

**Exempel:**

**Skicka som anpassad rubrik**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**Skicka som frågeparameter**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**Skickar som postparameter**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>Om Amazon SSO saknas eller är ogiltigt ignoreras attributet och anropen körs som om enkel inloggning inte finns.
