---
title: Lagra autentiseringsuppgifter
description: Lagra autentiseringsuppgifter
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Lagra autentiseringsuppgifter{#storing-credentials}

SDK har stöd för flera sätt att lagra autentiseringsuppgifter (ett certifikat för offentlig nyckel och tillhörande privat nyckel), bland annat på en HSM eller som en PKCS12-fil. Autentiseringsuppgifter används när den privata nyckeln krävs (till exempel för att paketeraren ska signera metadata eller för att licensservern ska dekryptera data som krypterats med licensservern eller den offentliga transportnyckeln). Privata nycklar måste övervakas noga för att säkerställa säkerheten för ditt innehåll och din licensserver. PKCS12 är ett standardformat för en fil som innehåller en referens som krypterats med ett lösenord. Filtillägget .pfx används vanligtvis för filer i det här formatet.

>[!NOTE]
>
>Adobe rekommenderar att du använder HSM för maximal säkerhet. Mer information finns i Riktlinjerna för säker distribution för Adobe Access.

>[!NOTE]
>
>Från och med Java1.7 har 64-bitars Sun Java för Windows inte stöd för de PKCS11-gränssnitt som krävs för att Adobe Access DRM ska kunna kommunicera med HSM-enheter. Om du tänker använda ett HSM-kort bör du använda en 32-bitarsversion av Java, eller använda en JDK som har stöd för de fullständiga PKCS1-gränssnitten.

Du kan behålla en privat nyckel på en HSM-modul (Hardware Security Module) och använda SDK för att skicka de autentiseringsuppgifter du får från HSM. Om du vill använda en referens som lagras på en HSM använder du en JCE-leverantör som kan kommunicera med en HSM för att få en referens till den privata nyckeln. Skicka sedan handtaget för den privata nyckeln, providernamnet och certifikatet som innehåller den offentliga nyckeln till `ServerCredentialFactory.getServerCredential()`.

SunPKCS11-providern är ett exempel på en JCE-leverantör som kan användas för att komma åt en privat nyckel på en HSM (se Sun Java-dokumentationen för instruktioner om hur du använder den här providern). Vissa HSM-moduler har också en Java SDK som innehåller en JCE-leverantör.

PEM och DER är två sätt att koda ett certifikat för offentlig nyckel. PEM är en base-64-kodning och DER är en binär kodning. Certifikatfiler har vanligtvis filnamnstillägget .cer, .pem. eller .der. Certifikat används på platser där endast den offentliga nyckeln krävs. Om en komponent bara kräver den offentliga nyckeln för att fungera är det bättre att ge den komponenten certifikatet i stället för en autentiserings- eller PKCS12-fil.
