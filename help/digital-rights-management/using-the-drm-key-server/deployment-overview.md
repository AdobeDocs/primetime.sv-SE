---
title: Distribuera en översikt över nyckelservern Primetime DRM
description: Distribuera en översikt över nyckelservern Primetime DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# Distribuera Primetime DRM Key Server {#deploy-the-primetime-drm-key-server}

Innan du distribuerar nyckelservern Primetime DRM måste du kontrollera att du har installerat de nödvändiga versionerna av Java och Tomcat. Se, [DRM-serverkrav](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Nedladdningen av Primetime DRM Key Server innehåller [!DNL faxsks.war]. Om du vill distribuera WAR-filen kopierar du filen till Tomcat&#39;s [!DNL webapps] katalog. Om du tidigare har distribuerat WAR-filen kan du behöva ta bort den opackade WAR-katalogen manuellt, [!DNL faxsks] på Tomcat&#39;s [!DNL webapps] ). Om du vill förhindra att Tomcat packar upp WAR-filer redigerar du [!DNL server.xml] fil i Tomcat&#39;s [!DNL conf] och ange `unpackWARs` attribut till `false`.

Primetimes DRM-nyckelserver har ett plattformsspecifikt bibliotek (`jsafe.dll` i Windows eller `libjsafe.so` i Linux) för bättre prestanda. Kopiera rätt bibliotek för din plattform från `thirdparty/cryptoj/platform` till en plats som anges av `PATH` miljövariabel (eller `LD_LIBRARY_PATH` i Linux).

>[!NOTE]
>
>64-bitarsversionen av [!DNL jsafe] bör bara användas om både operativsystemet och JDK har stöd för 64-bitarsversionen, annars används 32-bitarsversionen.

## SSL-konfiguration {#ssl-configuration}

SSL krävs för fjärradministration av HTTPS-nycklar. SSL-anslutningarna kan hanteras av programservern (d.v.s. genom att konfigurera SSL i Tomcat) eller hanteras på en annan server (t.ex. en belastningsutjämnare, SSL-accelerator eller Apache). Fjärradministration av HTTPS-nycklar kräver en SSL-anslutning. Servern behöver ett SSL-certifikat som har utfärdats av en betrodd certifikatutfärdare.

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

Kopiera [!DNL server.cer]och [!DNL server.key] till Tomcat-katalogen. Ange följande anslutning i [!DNL conf/server.xml]:

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

* `KeyServer.ConfigRoot` - Den här katalogen innehåller alla konfigurationsfiler för Primetime DRM Key Server. Mer information om innehållet i dessa filer finns i [Konfigurationsfiler för nyckelservrar](#key-server-configuration-files). Om den inte anges är standardvärdet [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Detta är en loggkatalog som innehåller programloggar för iOS Key Server. Om den inte anges är standardinställningen densamma som `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Det här är en loggkatalog som innehåller programloggarna för Xbox Key Server. Om den inte anges är standardinställningen densamma som `KeyServer.ConfigRoot`.

Om du använder [!DNL catalina.bat] eller [!DNL catalina.sh] för att starta Tomcat kan dessa systemegenskaper enkelt anges med `JAVA_OPTS` miljövariabel. Alla Java-alternativ som anges här kommer att användas när Tomcat startas. Ange till exempel:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM-autentiseringsuppgifter {#primetime-drm-credentials}

Om du vill bearbeta nyckelbegäranden från Primetime DRM iOS- och Xbox 360-klienter måste Primetimes DRM-nyckelserver konfigureras med en uppsättning autentiseringsuppgifter som utfärdats av Adobe. Dessa autentiseringsuppgifter kan antingen lagras i PKCS#12 ( [!DNL .pfx]) eller på en HSM.

The [!DNL .pfx] filer kan finnas var som helst, men för att underlätta konfigurationen rekommenderar Adobe att du placerar [!DNL .pfx] filer i klientens konfigurationskatalog. Mer information finns i [Konfigurationsfiler för nyckelservrar](#key-server-configuration-files).

### HSM-konfiguration {#section_13A19E3E32934C5FA00AEF621F369877}

Om du väljer att använda en HSM för att lagra serverinloggningsuppgifterna måste du läsa in de privata nycklarna och certifikaten till HSM och skapa en *pkcs11.cfg* konfigurationsfil. Den här filen måste finnas i *KeyServer.ConfigRoot* katalog. Se `<Primetime DRM Key Server>/configs` katalog för ett exempel på PKCS 11-konfigurationsfil. Information om formatet för [!DNL pkcs11.cfg]finns i dokumentationen till Sun PKCS11-providern.

För att verifiera att HSM- och Sun PKCS1-konfigurationsfilerna är korrekt konfigurerade kan du använda följande kommando från katalogen där [!DNL pkcs11.cfg] filen finns ( [!DNL keytool] installeras med Java JRE och JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du ser dina autentiseringsuppgifter i listan är HSM korrekt konfigurerat och nyckelservern kan komma åt autentiseringsuppgifterna.

## Konfigurationsfiler för nyckelservrar {#key-server-configuration-files}

Nyckelservern Primetime DRM kräver två typer av konfigurationsfiler:

* En global konfigurationsfil, [!DNL flashaccess-keyserver-global.xml]
* En klientkonfigurationsfil för varje klientorganisation, [!DNL flashaccess-keyserver-tenant.xml]

Om konfigurationsfilerna ändras måste servern startas om för att ändringarna ska börja gälla.

För att undvika att göra lösenord tillgängliga i klartext i konfigurationsfilerna måste alla lösenord som anges i den globala konfigurationsfilen och klientkonfigurationsfilen krypteras. Mer information om kryptering av lösenord finns i [*Lösenordsfasare* in *Använda Primetime DRM-servern för skyddad strömning*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

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

The [!DNL flashaccess-keyserver-global.xml] konfigurationsfilen innehåller inställningar som gäller alla klientorganisationer för nyckelservern. Den här filen måste finnas i `KeyServer.ConfigRoot`. Se [!DNL configs] katalog för ett exempel på global konfigurationsfil. Den globala konfigurationsfilen innehåller följande:

* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Se kommentarerna i den globala konfigurationsfilen som finns i `<Primetime DRM Key Server>/configs` för mer information.

## Konfigurationsfiler för innehavare {#tenant-configuration-files}

The [!DNL flashaccess-ioskeyserver-tenant.xml] och [!DNL flashaccess-xboxkeyserver-tenant.xml] konfigurationsfiler innehåller inställningar som gäller för en specifik innehavare av DRM-nyckelservern Primetime. Varje klientorganisation har en egen instans av dessa konfigurationsfiler som finns i [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Se [!DNL configs/faxsks/tenants/sampletenant] katalog för en exempelklientkonfigurationsfil.

Du kan ange alla filsökvägar i klientkonfigurationsfilen som antingen absoluta sökvägar eller sökvägar i förhållande till klientens konfigurationskatalog ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Alla klientkonfigurationsfiler innehåller:

* Nyckelserverautentiseringsuppgifter - Anger en eller flera nyckelserverautentiseringsuppgifter (certifikat och privat nyckel) som utfärdas av Adobe. Kan anges som en sökväg till en [!DNL .pfx] fil och ett lösenord eller ett alias för en autentiseringsuppgift som lagras på en HSM. Flera sådana autentiseringsuppgifter kan anges här, antingen som filsökvägar, nyckelalias eller både och.

The **iOS** Klientkonfigurationsfilen innehåller:

* Nyckelleveransfönster - (valfritt) Anger tidsstämpelgiltighetsfönstret för begäran om nyckelleverans (i sekunder). Standardvärdet är 500 sekunder.

The **Xbox 360** Klientkonfigurationsfilen innehåller:

* XSTS-autentiseringsuppgifter - Anger programutvecklarens autentiseringsuppgifter som används för att dekryptera XSTS-token
* XSTS-signeringscertifikat - Anger det certifikat som används för att verifiera signaturen på XSTS-tokens.
* Packager Tillåtelselista - Packager-certifikat som är betrodda av nyckelservern. Om det inte finns några paketerarcertifikat i listan betraktas alla paketerarcertifikat som tillförlitliga.

## Loggfiler {#log-files}

Loggfilerna som genereras av Primetime DRM Key Server-programmet ( [!DNL flashaccess-ioskeyserver_*.log] och [!DNL flashaccess-xboxkeyserver_*.log]) finns i den katalog som anges av `KeyServer.LogRoot`.

Loggfilerna urskiljs utifrån klienttyp. Det finns två loggar per klienttyp:

* An *åtkomstlogg* - Övervakar endast förfrågningar och svar.
* A *kontextlogg* - Innehåller detaljerade felmeddelanden och stackspår.

## Starta nyckelservern {#starting-the-key-server}

Starta Key Server genom att starta Tomcat.
