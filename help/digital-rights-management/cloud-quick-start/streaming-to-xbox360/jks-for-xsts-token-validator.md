---
title: Skapa JKS för en XSTS-validerare
description: Skapa JKS för en XSTS-validerare
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Skapa JKS för en XSTS-validerare{#create-jks-for-an-xsts-validator}

1. Ta reda på det privata certifikatets aliasnamn, som finns i partnern [!DNL .pfx] -fil.

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

1. Put [!DNL xsts.jks] i din hemkatalog för Tomcat och definiera `-Dxsts-keystore-password=****` för Tomcat.

If [!DNL xsts_partner_cert.pfx] och [!DNL xsts.jks] använder olika lösenord, uppdatera `xsts` lösenord i `jks` för att göra dem likadana.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
