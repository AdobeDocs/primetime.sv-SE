---
description: Du konfigurerar Adobe® Access™ genom att kopiera filer från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Begär dessutom ett certifikat från Adobe Systems Incorporated. Du får flera autentiseringsuppgifter som används för att skydda integriteten för paketerat innehåll, licenser och kommunikation mellan klienten och servern.
seo-description: Du konfigurerar Adobe® Access™ genom att kopiera filer från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Begär dessutom ett certifikat från Adobe Systems Incorporated. Du får flera autentiseringsuppgifter som används för att skydda integriteten för paketerat innehåll, licenser och kommunikation mellan klienten och servern.
seo-title: Konfigurera utvecklingsmiljön
title: Konfigurera utvecklingsmiljön
uuid: 1f192783-9c9a-4342-909a-4881248a85ad
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Konfigurera SDK {#setting-up-the-sdk}

Du konfigurerar Adobe® Access™ genom att kopiera filer från dvd-skivan. Dessa filer innehåller JAR-filer som innehåller kod, certifikat och klasser från tredje part. Begär dessutom ett certifikat från Adobe Systems Incorporated. Du får flera autentiseringsuppgifter som används för att skydda integriteten för paketerat innehåll, licenser och kommunikation mellan klienten och servern.

Adobe Access SDK finns i två typer:
* Adobe Access Core SDK
* Adobe Access Professional SDK

I följande tabell visas en grundläggande jämförelse av SDK:er för Adobe Access:

| Funktion | Adobe Access Core SDK | Adobe Access Professional SDK |
|---|---|---|
| Flash Access 2.0 - funktioner | Tillgänglig | Tillgänglig |
| Nyckelrotation | - | Tillgänglig |
| Domänstöd | Tillgänglig | Tillgänglig |
| Förbättrad licenskedja | Tillgänglig | Tillgänglig |
| Synkroniseringsmeddelanden | Tillgänglig | Tillgänglig |
| Förgenerering av licens | Tillgänglig | Tillgänglig |
| Inbäddade licenser | Tillgänglig | Tillgänglig |

## Konfigurera utvecklingsmiljön {#setting-up-the-development-environment}

Kopiera från dvd-skivan följande SDK-filer för användning i utvecklingsmiljön och Java-klassökvägen:

* adobe-flashaccess-certs.jar (innehåller rotcertifikat från Adobe)
* adobe-flashaccess-sdk.jar (innehåller Adobe Access Core SDK-klasser)
* adobe-flashaccess-sdk-pro.jar (innehåller Adobe Access Professional SDK-klasser som endast krävs för Professional-funktioner)

Du behöver följande JAR-filer från tredje part som också finns på dvd:n i mappen &quot;thirdparty&quot; i SDK:

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-log-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

För bättre prestanda kan du som tillval aktivera inbyggt stöd för kryptografiska åtgärder genom att distribuera de plattformsspecifika biblioteken i mappen&quot;Third party/cryptoj&quot; i SDK. Om du vill aktivera inbyggt stöd lägger du till biblioteket för din plattform (jsafe.dll för Windows eller libjsafe.so för Linux) i sökvägen. 32- och 64-bitarsversionerna av dessa bibliotek tillhandahålls. (Observera att 64-bitarsversionen endast bör användas om du har ett 64-bitarsoperativsystem och du kör 64-bitarsversionen av Java).

En del av SDK är dessutom adobe-flashaccess-lcrm.jar (tillval). Den här filen behövs bara för funktioner som är relaterade till FMRMS (Adobe Media Rights Management Server) 1.x-kompatibilitet. Om du tidigare har distribuerat FMRMS 1.x och inte vill paketera om ditt FMRMS-skyddade innehåll måste du lägga till stöd till licensservern så att den kan hantera gammalt innehåll och klienter.
