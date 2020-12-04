---
seo-title: Generera en CSR-fil (Certificate Signing Request)
title: Generera en CSR-fil (Certificate Signing Request)
uuid: 04abd5d2-77ac-4f89-8bea-31d389159aee
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Generera en CSR-fil (Certificate Signing Request) {#generate-a-certificate-signing-request-requester}

1. Skapa ett nyckelpar. Om du vill använda ett verktyg som OpenSSL öppnar du ett kommandofönster och anger följande:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe rekommenderar att du inkluderar certifikattypen (lic, pkgr, trans, trial eller eval) i nyckelnamnet. Den här namnkonventionen gör det enklare att distribuera dem på licensservern. I det här exemplet används&quot;mycompany-license.key&quot;. För utvärderings- och testversionerna använder du&quot;mincompany-eval.key&quot; och&quot;mincompany-trial.key&quot;.

1. Ange ett lösenord för att skydda den privata nyckeln.

   Lösenord måste innehålla minst 12 tecken. Tecknen ska innehålla en blandning av ASCII-tecken och siffror i versaler och gemener. Om du vill använda OpenSSL för att generera ett starkt lösenord öppnar du ett kommandofönster och anger följande:

   ```
   openssl rand -base64 8
   ```

1. Skapa en CSR-begäran (Certificate Signing Request).

   Om du vill använda OpenSSL för att generera en CSR-fil öppnar du ett kommandofönster och anger följande:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Du uppmanas att ange lösenordet för den privata nyckeln.
1. Skapa en säkerhetskopia av din privata nyckel och lösenord.

   Om du tappar bort den privata nyckeln eller om den har komprometterats kontaktar du certifikatadministratören i Adobe för att återkalla certifikatet och begära ett nytt.

   >[!NOTE]
   >
   >Adobe rekommenderar att du använder en HSM för att skydda din privata nyckel och ditt lösenord.

