---
seo-title: Lagra autentiseringsuppgifter
title: Lagra autentiseringsuppgifter
uuid: a9e9db72-c921-4c28-ad1d-3fd3c2283f14
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lagra autentiseringsuppgifter{#storing-credentials}

Primetimes DRM SDK har stöd för olika sätt att lagra autentiseringsuppgifter, bland annat via en HSM-modul (Hardware Security Module) eller som en PKCS12-fil. SDK använder en autentiseringsuppgift (certifikat för offentlig nyckel och associerad privat nyckel) när den privata nyckeln krävs. Paketeraren använder till exempel en autentiseringsuppgift för att signera metadata. License Server använder en autentiseringsuppgift för att dekryptera data som har krypterats med den offentliga nyckeln för licensservern eller transport.

Du måste noga bevaka privata nycklar för att säkerställa säkerheten för ditt innehåll och licensservern. PKCS12 är ett standardfilformat för arkivering av inloggningsuppgifter som har krypterats med ett lösenord. (Du kan också kryptera och signera själva PKCS12-filen.) Filtillägget [!DNL .pfx] används vanligtvis för filer som har stöd för det här formatet.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Adobe rekommenderar att du använder en HSM för maximal säkerhet.
>
>Se *Adobe Primetimes riktlinjer* för säker distribution av DRM.

>[!NOTE] {prioritet=&quot;high&quot;}
>
>Från och med Java 1.7 har 64-bitars Sun Java för Windows inte längre stöd för de PKCS11-gränssnitt som krävs för Primetime DRM för kommunikation med HSM-enheter. Om du tänker använda ett HSM-kort måste du använda en 32-bitarsversion av Java, eller använda en JDK som har stöd för de fullständiga PKCS1-gränssnitten.

Du kan behålla en privat nyckel på en HSM och använda Primetimes DRM SDK för att skicka de autentiseringsuppgifter som du får från HSM. Om du vill använda en referens som lagras på en HSM måste du använda en JCE-leverantör som kan kommunicera med en HSM för att få en referens till den privata nyckeln. Sedan måste du skicka handtaget för den privata nyckeln, providernamnet och certifikatet som innehåller den offentliga nyckeln till `ServerCredentialFactory.getServerCredential()`.

SunPKCS11-providern representerar ett exempel på en JCE-leverantör som du kan använda för att komma åt en privat nyckel på en HSM. Vissa HSM-moduler ingår också i en Java SDK som medföljer en JCE-leverantör.

I dokumentationen för Sun Java finns instruktioner om hur du använder den här providern.

PEM och DER är sätt att koda ett certifikat för offentlig nyckel. PEM är en base-64-kodning och DER är en binär kodning. Certifikatfiler använder vanligtvis tillägget [!DNL .cer], [!DNL .pem]eller [!DNL .der]. Certifikat används där bara en offentlig nyckel krävs. Om en komponent endast kräver den offentliga nyckeln för att fungera, rekommenderar vi att du tillhandahåller komponenten certifikatet i stället för en autentiserings- eller PKCS12-fil.
