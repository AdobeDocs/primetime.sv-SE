---
seo-title: Skapa JKS för en XSTS-validerare
title: Skapa JKS för en XSTS-validerare
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Skapa JKS för en XSTS-validerare{#create-jks-for-an-xsts-validator}

1. Ta reda på det privata certifikatets aliasnamn, som finns i partnerfilen [!DNL .pfx].

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

1. Placera [!DNL xsts.jks] i din Tomcat-arbetskatalog och definiera `-Dxsts-keystore-password=****` för Tomcat.

Om [!DNL xsts_partner_cert.pfx] och [!DNL xsts.jks] använder olika lösenord ska du uppdatera `xsts`-lösenordet i `jks` så att de blir samma.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
