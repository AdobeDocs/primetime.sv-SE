---
seo-title: XSTS-tokenvalidering för Xbox Live
title: XSTS-tokenvalidering för Xbox Live
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# XSTS-tokenvalidering för Xbox Live{#xbox-live-xsts-token-validation}

För XSTS-begäranden innehåller `customerSpecificAuthToken` fältet Base64-kodad XSTS-token. I exempelkoden `XSTSValidator` undersöks Base64-avkodad token för förekomsten av `EncryptedAssertion` elementet. Du kan dock använda andra metoder för att skilja mellan dessa förfrågningar och förfrågningar som inte kommer från Xbox. Du kan till exempel använda en annan URL.

Den princip som returneras i svarsmeddelandet åsidosätter den ursprungliga principen i de DRM-metadata som medföljer Xbox-nyckelbegäran. Endast en deluppsättning av principfunktioner stöds av Xbox-klienten och dessa fält är de enda som kommer att åsidosätta den ursprungliga principen.

Ytterligare installationssteg krävs för att stödja tokendekryptering och validering. Du måste läsa in [!DNL xsts_partner_cert.pfx] och [!DNL x_secure_token_service.part.xboxlive.com.cer] inloggningsuppgifter i en nyckelbehållare i JKS-format, som du sedan anger som systemegenskap för den bakomliggande tillståndsservern `xsts-keystore`. Som standard [!DNL .pfx] har partnern aliaset `xsts`och tokenvalideringscertifikatet aliaset `xsts-verify-cert`. Du kan även åsidosätta dessa med hjälp av systemegenskaper. Slutligen finns det en systemegenskap `xsts-keystore-password` som inte har någon standardegenskap och som innehåller nyckelbehållarlösenordet. De systemegenskaper som läses av `XSTSValidator` koden sammanfattas nedan:

| Systemegenskap | Standardvärde | Kommentar |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | JKS-formatnyckelbehållare som används av valideraren. |
| `xsts-keystore-password` |  | Lösenord för nyckelbehållaren |
| `xsts-alias` | `xsts` | Alias som används för att hämta dekrypteringsnyckeln från nyckelbehållaren |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias som används för att hämta verifieringscertifikatet från nyckelbehållaren |

