---
title: Distribuera översikten över Primetime DRM Key Server
description: Distribuera översikten över Primetime DRM Key Server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Distribuera Primetime DRM-nyckelservern {#deploy-the-primetime-drm-key-server}

Innan du distribuerar nyckelservern Primetime DRM måste du kontrollera att du har installerat de nödvändiga versionerna av Java och Tomcat. Se [DRM Key Server Requirements](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Nedladdningen av Primetime DRM Key Server innehåller [!DNL faxsks.war]. Om du vill distribuera WAR-filen kopierar du filen till Tomcat&#39;s [!DNL webapps]-katalogen. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort den opackade WAR-katalogen ([!DNL faxsks] i Tomcat-katalogen [!DNL webapps]) manuellt. Om du vill hindra Tomcat från att packa upp WAR-filer redigerar du filen [!DNL server.xml] i Tomcat-katalogen [!DNL conf] och anger attributet `unpackWARs` till `false`.

Primetimes DRM Key Server har ett plattformsspecifikt bibliotek (`jsafe.dll` i Windows eller `libjsafe.so` i Linux) som tillval för förbättrade prestanda. Kopiera lämpligt bibliotek för din plattform från `thirdparty/cryptoj/platform` till en plats som anges av miljövariabeln `PATH` (eller `LD_LIBRARY_PATH` i Linux).

>[!NOTE]
>
>64-bitarsversionen av [!DNL jsafe]-biblioteket bör bara användas om både operativsystemet och JDK har stöd för 64-bitarsversionen, annars använder du 32-bitarsversionen.

## SSL-konfiguration {#ssl-configuration}

SSL krävs för fjärradministration av HTTPS-nyckel. SSL-anslutningarna kan hanteras av programservern (d.v.s. genom att konfigurera SSL i Tomcat) eller hanteras på en annan server (d.v.s. en belastningsutjämnare, SSL-accelerator eller Apache). Fjärradministration av HTTPS-nycklar kräver en SSL-anslutning. Servern behöver ett SSL-certifikat som har utfärdats av en betrodd certifikatutfärdare.

Det finns många alternativ för att konfigurera SSL. Nedan visas exempel på hur SSL konfigureras med klientautentisering i Apache och Tomcat.

I följande exempel visas Apache SSL-konfigurationen:

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

I följande exempel visas Tomcat SSL-konfigurationen. Så här skapar du certifikat- och nyckelfiler:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

När du uppmanas att ange ett vanligt namn använder du serverns fullständiga kvalificerade domännamn (FQDN).

Kopiera [!DNL server.cer] och [!DNL server.key] till Tomcat-katalogen. Ange följande koppling i [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java-systemegenskaper {#java-system-properties}

Du kan ange följande två Java-systemegenskaper för att ändra platsen för konfigurations- och loggfiler för Primetimes DRM-nyckelserver:

* `KeyServer.ConfigRoot` - Den här katalogen innehåller alla konfigurationsfiler för Primetime DRM Key Server. Mer information om innehållet i dessa filer finns i [Konfigurationsfiler för nyckelserver](#key-server-configuration-files). Om den inte anges är standardvärdet [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Detta är en loggkatalog som innehåller programloggar för iOS Key Server. Om den inte anges är standardvärdet samma som `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Det här är en loggkatalog som innehåller programloggarna för Xbox Key Server. Om den inte anges är standardvärdet `KeyServer.ConfigRoot`.

Om du använder [!DNL catalina.bat] eller [!DNL catalina.sh] för att starta Tomcat kan du enkelt ange de här systemegenskaperna med hjälp av miljövariabeln `JAVA_OPTS`. Alla Java-alternativ som anges här kommer att användas när Tomcat startas. Ange till exempel:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM-autentiseringsuppgifter {#primetime-drm-credentials}

Om du vill bearbeta nyckelbegäranden från Primetime DRM iOS- och Xbox 360-klienter måste Primetime DRM Key Server konfigureras med en uppsättning autentiseringsuppgifter som utfärdas av Adobe. Dessa autentiseringsuppgifter kan antingen lagras i PKCS#12-filer ( [!DNL .pfx]) eller på en HSM.

[!DNL .pfx]-filerna kan finnas var som helst, men för att konfigurationen ska bli enkel rekommenderar Adobe att du placerar [!DNL .pfx]-filerna i klientens konfigurationskatalog. Mer information finns i [Konfigurationsfiler för nyckelservrar](#key-server-configuration-files).

### HSM-konfiguration {#section_13A19E3E32934C5FA00AEF621F369877}

Om du väljer att använda en HSM för att lagra serverinloggningsuppgifterna måste du läsa in de privata nycklarna och certifikaten på HSM och skapa en *pkcs11.cfg*-konfigurationsfil. Filen måste finnas i katalogen *KeyServer.ConfigRoot*. Se katalogen `<Primetime DRM Key Server>/configs` för ett exempel på en PKCS 11-konfigurationsfil. Mer information om formatet för [!DNL pkcs11.cfg] finns i dokumentationen för Sun PKCS11-providern.

För att verifiera att konfigurationsfilerna för HSM och Sun PKCS1 är korrekt konfigurerade kan du använda följande kommando från katalogen där [!DNL pkcs11.cfg]-filen finns ( [!DNL keytool] installeras med Java JRE och JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du ser dina inloggningsuppgifter i listan är HSM korrekt konfigurerat och nyckelservern kan komma åt inloggningsuppgifterna.

## Konfigurationsfiler för nyckelservern {#key-server-configuration-files}

Nyckelservern Primetime DRM kräver två typer av konfigurationsfiler:

* En global konfigurationsfil, [!DNL flashaccess-keyserver-global.xml]
* En klientkonfigurationsfil för varje klientorganisation, [!DNL flashaccess-keyserver-tenant.xml]

Om konfigurationsfilerna ändras måste servern startas om för att ändringarna ska börja gälla.

För att undvika att göra lösenord tillgängliga i klartext i konfigurationsfilerna måste alla lösenord som anges i den globala konfigurationsfilen och klientkonfigurationsfilen krypteras. Mer information om kryptering av lösenord finns i [*Lösenordssparare* i *Använda Primetime DRM-servern för skyddad direktuppspelning*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## Konfigurationskatalogstruktur {#configuration-directory-structure}

Konfigurationskatalogerna har följande struktur:

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## Global konfigurationsfil {#global-configuration-file}

Konfigurationsfilen [!DNL flashaccess-keyserver-global.xml] innehåller inställningar som gäller alla klientorganisationer för nyckelservern. Filen måste finnas i `KeyServer.ConfigRoot`. I katalogen [!DNL configs] finns ett exempel på en global konfigurationsfil. Den globala konfigurationsfilen innehåller följande:

* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Mer information finns i kommentarerna i den globala konfigurationsfilen som finns i `<Primetime DRM Key Server>/configs`.

## Konfigurationsfiler för klientorganisation {#tenant-configuration-files}

Konfigurationsfilerna [!DNL flashaccess-ioskeyserver-tenant.xml] och [!DNL flashaccess-xboxkeyserver-tenant.xml] innehåller inställningar som gäller för en specifik innehavare av nyckelservern Primetime DRM. Varje klientorganisation har en egen instans av dessa konfigurationsfiler som finns i [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. I katalogen [!DNL configs/faxsks/tenants/sampletenant] finns ett exempel på en klientkonfigurationsfil.

Du kan ange alla filsökvägar i klientkonfigurationsfilen som antingen absoluta sökvägar eller sökvägar i förhållande till klientens konfigurationskatalog ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Alla klientkonfigurationsfiler innehåller:

* Nyckelserverautentiseringsuppgifter - Anger en eller flera nyckelserverautentiseringsuppgifter (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en [!DNL .pfx]-fil och ett lösenord, eller ett alias för en autentiseringsuppgift som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

Klientkonfigurationsfilen för **iOS** innehåller:

* Nyckelleveransfönster - (valfritt) Anger tidsstämpelgiltighetsfönstret för begäran om nyckelleverans (i sekunder). Standardvärdet är 500 sekunder.

Klientkonfigurationsfilen **Xbox 360** innehåller:

* XSTS-autentiseringsuppgifter - Anger programutvecklarens autentiseringsuppgifter som används för att dekryptera XSTS-token
* XSTS-signeringscertifikat - Anger det certifikat som används för att verifiera signaturen på XSTS-tokens.
* Packager Tillåtelselista - Packager-certifikat som är betrodda av nyckelservern. Om det inte finns några paketerarcertifikat i listan betraktas alla paketerarcertifikat som tillförlitliga.

## Loggfiler {#log-files}

Loggfilerna som genereras av Primetime DRM Key Server-programmet ( [!DNL flashaccess-ioskeyserver_*.log] och [!DNL flashaccess-xboxkeyserver_*.log]) finns i den katalog som anges av `KeyServer.LogRoot`.

Loggfilerna urskiljs utifrån klienttyp. Det finns två loggar per klienttyp:

* En *åtkomstlogg* - Övervakar endast begäranden och svar.
* En *kontextlogg* - Innehåller detaljerade felmeddelanden och stackspårningar.

## Startar nyckelservern {#starting-the-key-server}

Starta Key Server genom att starta Tomcat.