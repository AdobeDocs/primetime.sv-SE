---
title: Integrera medietokenverifieraren
description: Integrera medietokenverifieraren
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Integrera medietokenverifieraren

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Om Media Token Verifier {#about-media-token-verifier}

När auktoriseringen lyckas skapar Adobe Primetime-autentiseringen en AuthZ-token (long-life authentication).  AuthZ-token skickas antingen till klientsidan eller lagras på serversidan, beroende på klientens plattform.  (Se [Förstå token](/help/authentication/programmer-overview.md#understanding-tokens) för hur tokens lagras på olika klientsystem, tillsammans med annan information.)


En AuthZ-token tillåter användaren av platsen att visa en given resurs.  Den har en normal TTL (time-to-live) på 6 till 24 timmar, varefter denna token upphör att gälla. **För faktisk visningsåtkomst använder Primetime-autentiseringen AuthZ-token för att generera en kort medietoken som du får och skickar till medieservern**. Dessa kortlivade medietokens har en mycket kort TTL (vanligtvis några minuter).


I AccessEnabler-integrationer får du den kortlivade medietoken via `setToken()` återanrop. För klientlösa API-integrationer får du den kortlivade Media-token med `<SP_FQDN>/api/v1/tokens/media` API-anrop. Token är en sträng som skickas i klartext, signerad av Adobe, med tokenskydd baserat på PKI (Public Key Infrastructure). Med det här PKI-baserade skyddet signeras token med en asymmetrisk nyckel som utfärdas till Adobe av en certifikatutfärdare.


Eftersom det inte finns någon validering på klientsidan för denna token kan en illasinnad användare använda verktyg för att mata in falska `setToken()` samtal. Därför **inte** helt enkelt bygger på att `setToken()` har utlösts när man överväger om en användare är behörig eller inte. Du måste validera att själva den kortlivade variabeln är legitim. Verifieringsbiblioteket för medietoken används.


>[!TIP]
>
>Du måste skicka hela längden på den returnerade tokensträngen till Media Token Verifier för validering.

## Validera kortlivade token med Media Token Verifier {#validate-short-livedttokens}

Vi rekommenderar att programmerare skickar token till en webbtjänst som använder Media Token Verifier Library för att validera token innan videoströmmen startas. Den mycket korta TTL-värdet för kortlivade medietoken är definierad som tillräckligt lång för att tillåta klocksynkroniseringsproblem mellan servern som genererar token och servern som validerar token, men inte längre.



The [Media Token Verifier Library](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} finns för Primetimes autentiseringspartners.



Biblioteket för medietokentverifieraren finns i Java-arkivet `mediatoken-verifier-VERSION.jar`. Biblioteket definierar:

* Ett token-verification API (`ITokenVerifier` gränssnitt), med JavaDoc-dokumentation
* Den offentliga nyckel för Adobe som används för att verifiera att token verkligen kommer från Adobe
* En referensimplementering (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) som visar hur du använder Verifier API och hur du använder den offentliga nyckeln för Adobe i biblioteket för att verifiera dess ursprung


Arkivet innehåller alla beroenden och certifikatnyckelbehållare. Standardlösenordet för den inkluderade certifikatnyckelbehållaren är &quot;123456&quot;.

* Verifieringsbiblioteket kräver JDK version 1.5 eller senare.
* Använd den önskade JCE-providern för signaturalgoritmen SHA256WithRSA.


**Verifieringsbiblioteket måste vara det enda sättet som används för att analysera tokeninnehållet. Programmerare bör inte tolka token och extrahera själva data eftersom tokenformatet inte är garanterat och kan komma att ändras senare.** Det är bara API:t för verifieraren som garanterat fungerar korrekt. Tolkning av strängen direkt kan fungera tillfälligt, men orsaka problem i framtiden när formatet kan ändras. Verifierings-API:t hämtar information från token, till exempel:

* Är token giltig ( `isValid()` metod)?
* Resurs-ID som är knutet till token ( `getResourceID()` ); den kan jämföras med (och den ska matcha) den andra parametern i `setToken()` funktionsåteranrop. Om det inte matchar kan det tyda på bedrägligt beteende.
* Tiden då token utfärdades (`getTimeIssued()` metod).
* TTL (`getTimeToLive()` metod).
* Ett anonymiserat autentiserings-GUID togs emot från MVPD (`getUserSessionGUID()` metod).
* Distributörens ID som autentiserade användaren och, om så är fallet, det proxy-MVPD som tillhandahöll autentisering för distributören.

## Använda Verifier API {#using-verifier-api}

The `ITokenVerifier` -klassen definierar metoder som du använder för att validera tokenautenticiteten för en given resurs. Använd `ITokenVerifier` metoder för att analysera en token som tagits emot som svar på en `setToken()` begäran.


The `isValid()` är det primära sättet att validera en token. Det krävs ett argument, ett resurs-ID. Om du skickar ett null-resurs-ID validerar metoden bara tokens autenticitet och giltighetsperiod.


The `isValid()` returnerar ett av dessa statusvärden:



| VALID_TOKEN | Alla valideringar har slutförts |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | Tokenformatet är ogiltigt |
| INVALID_SIGNATURE | Det gick inte att verifiera tokenautentiseringen |
| TOKEN_EXPIRED | Token TTL är inte giltig |
| INVALID_RESOURCE_ID | Token är inte giltig för angiven resurs |
| ERROR_UNKNOWN | Token har inte verifierats än |

Ytterligare metoder ger specifik åtkomst till resurs-ID:t, utfärdandetiden och tidsåtgången för en given token.

* Använd `getResourceID()` för att hämta det resurs-ID som är associerat med token och jämföra det med det ID som returnerades från setToken()-begäran.
* Använd `getTimeIssued()` för att hämta den tidpunkt då token utfärdades.
* Använd `getTimeToLive()` för att hämta TTL.
* Använd `getUserSessionGUID()` för att hämta ett anonymiserat GUID som angetts av MVPD.
* Använd `getMvpdId()` för att hämta ID:t för det MVPD som autentiserade användaren.
* Använd `getProxyMvpdId()` för att hämta ID:t för det MVPD som autentiserade användaren.

## Exempelkod {#sample-code}

Medietoken Verifier-arkivet innehåller en referensimplementering (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) och ett exempel på hur API anropas med testklassen. Detta exempel (`com.adobe.entitlement.text.EntitlementVerifierTest.java`) visar hur tokenverifieringsbiblioteket är integrerat med en medieserver.


```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
