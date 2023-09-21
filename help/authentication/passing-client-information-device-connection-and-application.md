---
title: Skicka klientinformation (enhet, anslutning och program)
description: Skicka klientinformation (enhet, anslutning och program)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---

# Skicka klientinformation (enhet, anslutning och program) {#pass-client-info}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Omfång {#pass-client-info-scope}

Det här dokumentet samlar information och cookbooks för att skicka klientinformation (enhet, anslutning och program) från ett programmeringsprogram till Adobe Primetime Authentication REST API:er eller SDK:er.

Fördelarna med att tillhandahålla kundinformation är:

* Möjligheten att korrekt aktivera HBA (Home Base Authentication) för vissa enhetstyper och MVPD-program som stöder HBA.
* Möjligheten att korrekt tillämpa TTL:er för vissa enhetstyper (till exempel konfigurera längre TTL:er för autentiseringssessioner på tv-anslutna enheter).
* Möjlighet att på rätt sätt sammanställa affärsdata i uppdelade rapporter över olika enhetstyper med hjälp av ESM (Entitlement Service Monitoring).
* Hindrar möjligheten att tillämpa olika affärsregler korrekt (t.ex. nedbrytning) på specifika enhetstyper.

## Ökning {#pass-client-info-overview}

Klientinformationen består av:

* **Enhet** information om de maskin- och programvaruattribut som finns på den enhet från vilken användaren försöker använda programmerarinnehållet.
* **Anslutning** information om anslutningsattributen för den enhet från vilken användaren ansluter till Adobe Primetime autentiseringstjänster och/eller programmeringstjänster (t.ex. server-till-server-implementeringar).
* **Program** information om det registrerade programmet från vilket användaren försöker förbruka programmerarinnehållet.

Klientinformationen är ett JSON-objekt som skapats med nycklar som presenteras i följande tabell.

>[!NOTE]
>
>Följande **tangenter** är **obligatoriskt** som ska skickas i JSON-objektet för klientinformation: **modell**, **osName**.
>
>Följande tangenter har **begränsad** värden: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|   | Nyckel | Begränsad | Beskrivning | Möjliga värden |
|---|---|---|---|---|
|            | primärHardwareType | # Ja | Enhetens primära maskinvarutyp. | # The values are restricted: Camera DataCollectionTerminal Desktop EmbeddedNetworkModule eReader GamesConsole GeolocationTracker Glasses MediaPlayer MobilePhone PaymentTerminal PluginModem SetTopBox TV Tablet WirelessHotspot-färgkarta okänd |
| #mandatory | modell | Nej | Enhetens modellnamn. | t.ex. iPhone, SM-G930V, AppleTV osv. |
|            | version | Nej | Enhetens version. | t.ex. 2.0.1 osv. |
|            | tillverkare | Nej | Enhetens tillverkningsföretag/organisation. | t.ex. Samsung, LG, ZTE, Huawei, Motorola, Apple osv. |
|            | leverantör | Nej | Enhetens säljande företag/organisation. | t.ex. Apple, Samsung, LG, Google osv. |
| #mandatory | osName | # Ja | Enhetens operativsystemnamn. | # Värdena är begränsade: Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|            | osFamily | Ja | Enhetens operativsystemsgruppnamn. | # Värdena är begränsade: Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|            | osVendor | Nej | Enhetens operativsystemsleverantör. | Amazon Apple Google LG Microsoft Mozilla Nintendo Nokia Roku Samsung Sony Tizen Project |
|            | osVersion | Nej | Enhetens operativsystemversion. | t.ex. 10.2, 9.0.1 osv. |
|            | browserName | # Ja | Webbläsarens namn. | # The values are limited: Android Browser Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Symbian Browser |
|            | browserVendor | # Ja | Webbläsarens byggföretag/organisation. | # The values are restricted: Amazon Apple Google Microsoft Motorola Mozilla Netscape Nintendo Nokia Samsung Sony Ericsson |
|            | browserVersion | Nej | Enhetens webbläsarversion. | Exempel: 60.0.3112 |
|            | userAgent | Nej | Enhetens användaragent. | Exempel: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, t.ex. Gecko) Version/10.0.3 Safari/602.4.8 |
|            | displayWidth | Nej | Enhetens fysiska skärmbredd. |                                                                                                                                                                                                                                                                                                                                                           |
|            | displayHeight | Nej | Enhetens fysiska skärmhöjd. |                                                                                                                                                                                                                                                                                                                                                           |
|            | displayPpi | Nej | Enhetens pixeldensitet för fysisk skärm. | Exempel: 294 |
|            | diagonalScreenSize | Nej | Enhetens diagonala mått för fysisk skärm i tum. | t.ex. 5.5, 10.1 |
|            | connectionIp | Nej | Enhetens IP som används för att skicka HTTP-begäranden. | t.ex. 8.8.4.4 |
|            | connectionPort | Nej | Enhetens port som används för att skicka HTTP-begäranden. | till exempel 53124 |
|            | connectionType | Nej | Nätverksanslutningstypen. | t.ex. WiFi, LAN, 3G, 4G, 5G |
|            | connectionSecure | # Ja | Säkerhetsstatus för nätverksanslutning. | # Värdena är begränsade: true - om det är ett säkert nätverk som är false - om det är en offentlig aktiv punkt |
|            | applicationId | Nej | Programmets unika identifierare. | t.ex. CNN |

## API-referenser {#api-ref}

I det här avsnittet presenteras det API som hanterar klientinformation när du använder Adobe Primetime Authentication REST API:er eller SDK:er.

### REST API {#rest-api}

Adobe Primetime autentiseringstjänster har stöd för att ta emot klientinformationen på följande sätt:

* Som en **header: &quot;X-Device-Info&quot;**
* Som en **frågeparameter: &quot;device_info&quot;**
* Som en **post-parameter: &quot;device_info&quot;**

>[!IMPORTANT]
>
>I alla tre scenarierna måste rubrikens eller parameterns nyttolast vara **Base64-kodad och URL-kodad**.

**SDK**

#### JavaScript SDK {#js-sdk}

AccessEnabler JavaScript SDK skapar som standard ett JSON-objekt för klientinformation, som skickas till Adobe Primetime Authentication Services, om det inte åsidosätts.

JavaScript SDK för AccessEnabler har stöd för **åsidosätta endast** nyckeln &quot;applicationId&quot; från JSON-objektet för klientinformation via [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))&#39;s *applicationId* options-parameter.

>[!CAUTION]
>
>The `applicationId` parametervärdet måste vara ett oformaterat textsträngsvärde.
>Om programmerarprogrammet beslutar att skicka applicationId, kommer resten av klientinformationsnycklarna fortfarande att beräknas av AccessEnabler JavaScript SDK.

#### iOS/tvOS SDK {#ios-tvos-sdk}

AccessEnabler iOS/tvOS SDK skapar som standard ett JSON-objekt för klientinformation, som skickas till Adobe Primetime autentiseringstjänster, om det inte åsidosätts.

AccessEnabler iOS/tvOS SDK stöder **åsidosätta hela** JSON-objekt för klientinformation via [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)&#39;s device_info parameter.

>[!CAUTION]
>
>The *device_info* parametervärdet måste vara ett **Base64-kodad** *NSString* värde.
>
>Om Programmer-programmet beslutar att godkänna *device_info*, åsidosätts alla klientinformationsnycklar som beräknas av AccessEnabler iOS/tvOS SDK. Därför är det mycket viktigt att beräkna och skicka värdena för så många tangenter som möjligt. Mer information om implementeringen finns i [Ökning](#pass-client-info-overview) tabellen och [iOS/tvOS cookbook](#ios-tvos).

#### Android/FireOS SDK {#and-fire-os-sdk}

The `AccessEnabler` Android/FireOS SDK skapar som standard ett JSON-objekt för klientinformation, som skickas till Adobe Primetime autentiseringstjänster, om det inte åsidosätts.

The `AccessEnabler` Android/FireOS SDK stöder **åsidosätta hela** JSON-objekt för klientinformation via [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)&#39;s `device_info` parameter.

>[!NOTE]
>
>The `device_info` parametervärdet måste vara ett **Base64-kodad** Strängvärde.

>[!IMPORTANT]
>
>Om Programmer-programmet beslutar att godkänna `device_info`och sedan alla klientinformationsnycklar som beräknas av `AccessEnabler` Android/FireOS SDK åsidosätts. Därför är det mycket viktigt att beräkna och skicka värdena för så många tangenter som möjligt. Mer information om implementeringen finns i [Ökning](#pass-client-info-overview) tabellen och [Android](#android) och [FireOS](#fire-tv) kokbok.

## Cookbooks {#cookbooks}

I det här avsnittet presenteras en cookbook för att skapa JSON-objekt för klientinformation för olika enhetstyper.

>[!IMPORTANT]
>
>De tangenter som är markerade med  **!** är obligatoriska att skicka.

### Android {#android}

Enhetsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---------------|-----------------------------|---------------|
| ! | modell | Build.MODEL | GT-I9505 |
|   | leverantör | Build.BRAND | samsung |
|   | tillverkare | Build.MANUFACTURER | samsung |
| ! | version | Build.DEVICE | jflte |
|   | displayWidth | DisplayMetrics.widthPixels | 600 |
|   | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | hårdkodad | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

Anslutningsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|   | connectionSecure |                                                                                                                                                           |                                                                                           |

Programinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---------------|-----------|--------------|
|   | applicationId | hårdkodad | CNN |

>[!IMPORTANT]
>
Information om enheten, anslutningen och programmet måste läggas till i samma JSON-objekt. Efteråt måste det resulterande objektet **Base64-kodad**. För Adobe Primetime Authentication REST API:er måste värdet dessutom vara **URL-kodad**.

**Exempelkod**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
>
**Resurser:**
* public, klass [bygg](https://developer.android.com/reference/android/os/Build.html){target=_blank} i dokumentationen för Java-utvecklare.

### FireTV {#fire-tv}

Enhetsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (till exempel) |
|---|---------------|-----------------------------|--------------|
| ! | modell | Build.MODEL | AFTM |
|   | leverantör | Build.BRAND | Amazon |
|   | tillverkare | Build.MANUFACTURER | Amazon |
| ! | version | Build.DEVICE | montoya |
|   | displayWidth | DisplayMetrics.widthPixels |              |
|   | displayHeight | DisplayMetrics.heightPixels |              |
| ! | osName | hårdkodad | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

Anslutningsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|------------------|--------|---------------|
| ! | connectionType |        |               |
|   | connectionSecure |        |               |

Programinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---------------|-----------|--------------|
|   | applicationId | hårdkodad | CNN |

>[!IMPORTANT]
>
Information om enheten, anslutningen och programmet måste läggas till i samma JSON-objekt. Efteråt måste det resulterande objektet **Base64-kodad**. För Adobe Primetime Authentication REST API:er måste värdet dessutom vara **URL-kodad**.

>[!NOTE]
>
**Resurser:**
* public, klass [Bygge](https://developer.android.com/reference/android/os/Build.html){target=_blank} i dokumentationen för Android-utvecklare.
* [Identifiera FireTV-enheter](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}

### iOS/tvOS {#ios-tvos}

Enhetsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---------------|------------------------|--------------|
| ! | modell | uname.machine | iPhone |
|   | leverantör | hårdkodad | Apple |
|   | tillverkare | hårdkodad | Apple |
| ! | version | uname.machine | 8,1 |
|   | displayWidth | UIScreen.mainScreen | 320 |
|   | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

Anslutningsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [Tillgänglighet currentReachabilityStatus] |              |
|   | connectionSecure |                                           |              |


Programinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---------------|-----------|--------------|
|   | applicationId | hårdkodad | CNN |

>[!IMPORTANT]
>
Information om enheten, anslutningen och programmet måste läggas till i samma JSON-objekt. Efteråt måste det resulterande objektet vara Base64-kodat. För Adobe Primetime Authentication REST API:er måste värdet också vara URL-kodat.

**Exempelkod**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
>
**Resurser:**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [Om nåbarhet](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}

### Roku {#roku}

Enhetsinformationen kan utformas på följande sätt:

| Nyckel | Källa | Värde (exempel) |                 |
|-----|---------------|--------------------------------------------|-----------------|
| ! | modell | hårdkodad | &quot;Roku&quot; |
|     | leverantör | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
|     | tillverkare | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
| ! | version | ifDeviceInfo.GetModelDetails().ModelNumber | &quot;5303X&quot; |
|     | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|     | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | hårdkodad | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |                 |

Anslutningsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;, &quot;WiredConnection&quot; |
|   | connectionSecure | hårdkodad | true om anslutningen är kopplad |

Programinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---------------|-----------|--------------|
|   | applicationId | hårdkodad | CNN |

>[!IMPORTANT]
>
Information om enheten, anslutningen och programmet måste läggas till i samma JSON-objekt. Efteråt måste det resulterande objektet **Base64-kodad**. För Adobe Primetime Authentication REST API:er måste värdet också vara URL-kodat.

>[!NOTE]
>
Mer information finns i [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

Enhetsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Värde (exempel) |
|---|---|---|---|
| ! | modell | EasClientDeviceInformation.SystemProductName |                 |
|   | leverantör | hårdkodad | Microsoft |
|   | tillverkare | hårdkodad | Microsoft |
| ! | version | EasClientDeviceInformation.SystemHardwareVersion |                 |
|   | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|   | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |                 |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |                 |

Anslutningsinformationen kan utformas på följande sätt:

|   | Nyckel | Källa | Exempel |
|---|---|---|---|
| ! | connectionType |                                                   |                   |
|   | connectionSecure | NetworkAuthenticationType | &quot;Ingen&quot;, &quot;Wpa&quot; etc. |

Programinformationen kan utformas på följande sätt:

| Nyckel | Källa | Värde (exempel) |
|---|---|---|
| applicationId | hårdkodad | CNN |

>[!IMPORTANT]
>
Information om enheten, anslutningen och programmet måste läggas till i samma JSON-objekt. Efteråt måste det resulterande objektet **Base64-kodad**. För Adobe Primetime Authentication REST API:er måste värdet dessutom vara **URL-kodad**.

**Resurs**

* [Klassen EasClientDeviceInformation](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [Klassen DisplayInformation](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)
