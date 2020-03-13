---
description: 'null'
seo-description: 'null'
seo-title: Ange XSTS-token i spelaren
title: Ange XSTS-token i spelaren
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490

---


# Direktuppspelning till Xbox360 (tillval) {#streaming-to-xboc360}

Primetime DRM finns på Xbox360-plattformen. Det är dock bara användningsexemplet Skyddad strömning som stöds, inte hela sviten med DRM-principrättigheter. DRM-principrättigheter som inte direktuppspelas, t.ex. enhetsdomängrupper, stöds inte. Xbox360 ignorerar rättigheter som inte stöds vid uppspelning av innehåll.

Primetimes DRM-principrättigheter som stöds för Xbox är:
* Digital Output Protection
* Slutdatum för offlinecachelagring av licenser
* Startdatum för licens
* Licensens slutdatum
* Varaktighet för uppspelningsfönstret (sekunder)

Innehåll behöver kanske inte paketeras om för att strömma till Xbox360, om det redan har paketerats för en annan Primetime-plattform, till exempel iOS, Android eller Desktop.

En viktig fördel med Xbox360 är att den alltid måste nå ut till en nyckelserver varje gång en EXT-X-KEY-tagg påträffas i M3U8. Till skillnad från iOS, där en DRM-principinställning (policy.requireKeyServer) gör att videospelaren i iOS Primetime hämtar AES-dekrypteringsnyckeln från den lokala värden, försöker Xbox alltid hämta dekrypteringsnyckeln från en fjärrnyckelserver. Det finns ingen DRM-principrättighet att instruera Xbox-appen att hämta AES-dekrypteringsnyckeln från den lokala värden. På grund av detta krav måste EXT-X-KEY-posterna finnas i M3U8 som pekar på DRM-slutpunkten i Primetime Cloud. Den här URL:en anges via &lt;key_url> i konfigurationsfilen config_hls.xml för OfflinePackager.jar.

Om du vill paketera innehåll en gång och låta det direktuppspelas till alla Primetime-mål, samt konfigurera iOS-enheter så att de inte hämtar en nyckel från en fjärrnyckelserver, kan du paketera innehållet med en DRM-princip som har egenskapsprincipen.requireKeyServer=false (till exempel i policy_ios_localkeyserver.pol). iOS-enheter hämtar AES-nyckeln lokalt, medan Xbox-enheter ignorerar den här egenskapen och kontaktar Primetimes DRM-nyckelserver för en dekrypteringsnyckel.

>!Anteckning
>
>Alla Xbox360-begäranden måste använda anpassad autentisering/>Tillstånd.Det beror på att Xbox Live >använder en XSTS-token (Xbox Secure Token Server) för >autentisering på Xbox360-plattformen.
>DRM-licensservern i Primetime använder XSTS-token för att >validera integriteten för både Xbox-enheten och användaren som gör >licensförfrågan. För validering av XSTS-token krävs dock en >kundens privata Xbox Live-leverantörsnyckel, som inte lagras i Primetime Cloud DRM >s. Detta innebär att när Primetime Cloud DRM tar emot >en licensbegäran från en Xbox 360-klient, vidarebefordrar Primetime Cloud DRM >XSTS-token till Primetimes Back-End >Authentication/Entitlement-server. Primetimes kundserver
>tolkar och validerar sedan XSTS-token för att säkerställa att den är >signerad med kundens utgivarnyckel för program.
>Om du vill skicka en XSTS-token från Xbox360-klienten anger du token >synkront som svar på händelsen MediaPlayer.RequestKeyAttribute >som beskrivs närmare här: **Ange XSTS-token i spelaren.** Ett exempel på Back-End Authentication/Entitlement Server >ingår i programvaruversionen i katalogen Custom Authentication >och Entitlement.Validering av XSTS-tokens beskrivs här >närmare: Verifiering av XSTS-token för **Xbox Live.**


## Ange XSTS-token i spelaren {#set-the-xsts-token-in-your-player}

I Xbox360 anger du token asynkront som svar på `MediaPlayer.RequestKeyAttribute` händelsen.

Ange XSTS-token.

I exempelappen som medföljer programmet visas hur du ställer in XSTS-token i spelaren. Här är det relevanta kodfragmentet från exempelspelaren:

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## XSTS-tokenvalidering för Xbox Live {#xbox-live-xsts-token-validation}

För XSTS-begäranden innehåller `customerSpecificAuthToken` fältet Base64-kodad XSTS-token. I exempelkoden `XSTSValidator` undersöks Base64-avkodad token för förekomsten av `EncryptedAssertion` elementet. Du kan dock använda andra metoder för att skilja mellan dessa förfrågningar och förfrågningar som inte kommer från Xbox. Du kan till exempel använda en annan URL.

Den princip som returneras i svarsmeddelandet åsidosätter den ursprungliga principen i de DRM-metadata som medföljer Xbox-nyckelbegäran. Endast en deluppsättning av principfunktioner stöds av Xbox-klienten och dessa fält är de enda som kommer att åsidosätta den ursprungliga principen.

Ytterligare installationssteg krävs för att stödja tokendekryptering och validering. Du måste läsa in [!DNL xsts_partner_cert.pfx] och [!DNL x_secure_token_service.part.xboxlive.com.cer] inloggningsuppgifter i en nyckelbehållare i JKS-format, som du sedan anger som systemegenskap för den bakomliggande tillståndsservern `xsts-keystore`. Som standard [!DNL .pfx] har partnern aliaset `xsts`och tokenvalideringscertifikatet aliaset `xsts-verify-cert`. Du kan även åsidosätta dessa med hjälp av systemegenskaper. Slutligen finns det en systemegenskap `xsts-keystore-password` som inte har någon standardegenskap och som innehåller nyckelbehållarlösenordet. De systemegenskaper som läses av `XSTSValidator` koden sammanfattas nedan:

| Systemegenskap | Standardvärde | Kommentar |
|---|---|---|
| xsts-keystore | xsts.jks | JKS-formatnyckelbehållare som används av valideraren. |
| xsts-keystore-password |  | Lösenord för nyckelbehållaren |
| xsts-alias | xts | Alias som används för att hämta dekrypteringsnyckeln från nyckelbehållaren |
| xsts-verify-cert-alias | xsts-verify-cert | Alias som används för att hämta verifieringscertifikatet från nyckelbehållaren |

## Skapa JKS för en XSTS-validerare{#create-jks-for-an-xsts-validator}

1. Ta reda på det privata certifikatets aliasnamn, som finns i partnerfilen [!DNL .pfx] .

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Konvertera [!DNL .pfx] till [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (där `<alias>` är det privata certifikatets aliasnamn som du upptäckte i steg 1.)
1. Importera [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Lägg [!DNL xsts.jks] in din hemkatalog Tomcat och definiera `-Dxsts-keystore-password=****` för Tomcat.

Om [!DNL xsts_partner_cert.pfx] och [!DNL xsts.jks] använder olika lösenord kan du uppdatera `xsts` lösenordet i `jks` för att göra dem lika.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
