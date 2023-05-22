---
title: XSTS-tokenvalidering för Xbox Live
description: XSTS-tokenvalidering för Xbox Live
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# XSTS-tokenvalidering för Xbox Live{#xbox-live-xsts-token-validation}

För XSTS-förfrågningar: `customerSpecificAuthToken` fältet innehåller Base64-kodad XSTS-token. Provet `XSTSValidator` koden undersöker Base64-avkodad token för förekomsten av `EncryptedAssertion` element, Du kan dock använda andra metoder för att skilja mellan dessa förfrågningar och förfrågningar som inte kommer från Xbox. Du kan till exempel använda en annan URL.

Den princip som returneras i svarsmeddelandet åsidosätter den ursprungliga principen i de DRM-metadata som medföljer Xbox-nyckelbegäran. Endast en deluppsättning av principfunktioner stöds av Xbox-klienten och dessa fält är de enda som kommer att åsidosätta den ursprungliga principen.

Ytterligare installationssteg krävs för att stödja tokendekryptering och validering. Du måste läsa in [!DNL xsts_partner_cert.pfx] och [!DNL x_secure_token_service.part.xboxlive.com.cer] inloggningsuppgifter till en nyckelbehållare i JKS-format, som du sedan anger som systemegenskap för den bakomliggande tillståndsservern `xsts-keystore`. Som standard är partnern [!DNL .pfx] har aliaset `xsts`och tokenvalideringscertifikatet har aliaset `xsts-verify-cert`. Du kan även åsidosätta dessa med hjälp av systemegenskaper. Slutligen finns det en systemegenskap `xsts-keystore-password` som inte har något standardvärde och som innehåller nyckellösenordet. Systemegenskaperna som läses av `XSTSValidator` koden sammanfattas nedan:

| Systemegenskap | Standardvärde | Kommentar |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | JKS-formatnyckelbehållare som används av valideraren. |
| `xsts-keystore-password` |  | Lösenord för nyckelbehållaren |
| `xsts-alias` | `xsts` | Alias som används för att hämta dekrypteringsnyckeln från nyckelbehållaren |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias som används för att hämta verifieringscertifikatet från nyckelbehållaren |

