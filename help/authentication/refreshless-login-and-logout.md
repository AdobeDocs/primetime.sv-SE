---
title: Inloggning och utloggning utan uppdatering
description: Inloggning och utloggning utan uppdatering
exl-id: 3ce8dfec-279a-4d10-93b4-1fbb18276543
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---

# Inloggning och utloggning utan uppdatering {#tefresh-less-login-and-logout}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Översikt {#overview}

För webbprogram måste du ta hänsyn till några olika möjliga scenarier för autentisering och utloggning av användare.  MVPD-program kräver att användarna loggar in på MVPD:s webbsida för att autentisera, och dessutom spelas följande ytterligare faktorer upp:

- Vissa PDF-dokument kräver en fullständig omdirigering från din webbplats till inloggningssidan
- För vissa PDF-filer krävs att du öppnar en iFrame på din webbplats för att visa MVPD:s inloggningssida
- Vissa webbläsare hanterar inte iFrame-scenariot så för dessa webbläsare är ett bättre alternativ att använda ett popup-fönster i stället för iFrame

Före Adobe Primetime-autentisering 2.7 innebar alla dessa scenarier för autentisering av en användare en fullständig uppdatering av programmerarens sida.För version 2.7 och senare förbättrade Adobe Primetime autentiseringsteam dessa flöden så att användaren inte behöver se någon uppdatering av sidan i din app under inloggning och utloggning.  


## Detaljerad beskrivning {#detailed_description}

Låt oss börja med en sammanfattning av de ursprungliga autentiserings- och utloggningsflödena och sedan följa den med de förbättrade autentiserings- och utloggningsflödena. Observera att de första fyra avsnitten behandlar vanliga MVPD (non-TempPass), medan det sista avsnittet beskriver den speciella implementering som behöver tillämpas för TempPass:

- [Ursprungligt autentiseringsflöde](#orig_authn)
- [Ursprungligt utloggningsflöde](#orig_logout)
- [Förbättrat autentiseringsflöde](#improved_authn)
- [Förbättrat utloggningsflöde](#improved_logout)
- [TempPass-flöde](#improved_temppass)

</br>

## Ursprunglig autentisering/utloggningsflöden {#orig_authn}

**Autentisering**

Adobe Primetime webbklienter för autentisering har två sätt att autentisera, beroende på kraven för programmeringsdokument:

1. **Omdirigering av hela sidor -** När användaren har valt en leverantör (konfigurerad med helsidesomdirigering) från MVPD-väljaren på Programmerarens webbplats, `setSelectedProvider(<mvpd>)` anropas på AccessEnabler och användaren omdirigeras till MVPD:s inloggningssida. När användaren har angett giltiga inloggningsuppgifter dirigeras han/hon tillbaka till programmerarens webbplats. AccessEnabler initieras och autentiseringstoken hämtas från Adobe Primetime-autentisering under `setRequestor`.
1. **iFrame / Popup Window -** När användaren har valt en provider (konfigurerad med iFrame), `setSelectedProvider(<mvpd>)` anropas i AccessEnabler. Den här åtgärden aktiverar `createIFrame(width, height)` callback, meddela programmeraren att en iFrame (eller popup-meny - beroende på webbläsaren/inställningarna) ska skapas med namnet `"mvpdframe"` och de angivna måtten. När iFrame/popup har skapats läser AccessEnabler in MVPD:s inloggningssida i iFrame/popup. Användaren anger giltiga inloggningsuppgifter och iFrame/popup omdirigeras till Adobe Primetime-autentisering, som returnerar ett JS-fragment som stänger iFrame/popup och läser in den överordnade sidan (programmerarens webbplats). På samma sätt som för flöde 1 hämtas autentiseringstoken under `setRequestor`. 

The `displayProviderDialog` återanrop (utlöses av `getAuthentication`/`getAuthorization`) returnerar en lista över de virtuella dokumentdokumenten och deras lämpliga inställningar. The `iFrameRequired` egenskapen för en MVPD gör att programmeraren kan veta om den ska aktivera flöde 1 eller flöde 2. Observera att programmeraren krävs för att utföra en extra åtgärd (skapa en iFrame/popup) endast för flöde 2.

**Avbryt autentisering**

Det finns också en situation där användaren uttryckligen avbryter autentiseringsflödet genom att stänga inloggningssidan. Här är scenarierna och den föreslagna lösningen för programmerarna:

1. **Omdirigering av hela sidor -** När inloggningssidan stängs måste användaren navigera till programmerarens webbplats igen och initiera hela flödet från början. Ingen explicit åtgärd krävs på programmerarens sida i det här scenariot.
1. **iFrame -** Programmeraren rekommenderas att ha iFrame inuti en `div` (eller liknande UI-komponent) som har en stängningsknapp kopplad till sig. När användaren trycker på stängningsknappen kommer programmeraren att förstöra iFrame tillsammans med det associerade användargränssnittet och utföra `setSelectedProvider(null)`. Detta anrop gör att AccessEnabler kan rensa sitt interna tillstånd och gör det möjligt för användaren att initiera ett efterföljande autentiseringsflöde. `setAuthenticationStatus` och `sendTrackingData(AUTHENTICATION_DETECTION...)` aktiveras för att signalera ett misslyckat autentiseringsflöde (båda på `getAuthentication` och `getAuthorization`).
1. **Popup -** I vissa webbläsare går det inte att identifiera fönsterstängningshändelsen korrekt. Därför måste en annan metod användas här (till skillnad från iFrame-flödet ovan). Adobe rekommenderar att Programmeraren initierar en timer som regelbundet verifierar om inloggningsfönstret finns. Om fönstret inte finns kan programmeraren vara säker på att användaren manuellt har avbrutit inloggningsflödet och programmeraren kan fortsätta att ringa `setSelectedProvider(null)`. De utlösta återanropen är samma som i flöde 2 ovan.

</br>

## Ursprungligt utloggningsflöde {#orig_logout}

Utloggnings-API:t för AccessEnabler rensar bibliotekets lokala status och läser in MVPD:s utloggnings-URL i den aktuella fliken/fönstret. Webbläsaren går till MVPD:s utloggningsslutpunkt och när processen är klar dirigeras användaren tillbaka till programmerarens webbplats. Den enda åtgärd som krävs för användarens räkning är att trycka på knappen/länken Logga ut och initiera flödet. ingen användarinteraktion krävs för MVPD:s utloggningsslutpunkt.

**Ursprunglig autentisering/utloggningsflöde med siduppdatering**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## Förbättrad (utan uppdatering) autentisering {#improved_authn}

>[!NOTE]
>
>De förbättrade, uppdateringsfria inloggnings- och utloggningsflödena kräver att webbläsaren stöder moderna HTML5-tekniker, inklusive webbmeddelanden.

Både autentiserings- (inloggnings-) och utloggningsflödena ovan ger en liknande användarupplevelse genom att huvudsidan läses in igen när varje flöde har slutförts.  Den aktuella funktionen syftar till att förbättra användarupplevelsen genom att tillhandahålla en inloggning och inloggning utan uppdatering (bakgrund). Programmeraren kan aktivera/inaktivera inloggning och utloggning i bakgrunden genom att skicka två booleska flaggor (`backgroundLogin` och `backgroundLogout`) till `configInfo` parametern för `setRequestor` API. Som standard är inloggning/utloggning i bakgrunden inaktiverad (vilket ger kompatibilitet med den tidigare implementeringen).

**Exempel:**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**Autentisering**

Följande punkter beskriver övergången mellan de ursprungliga autentiseringsflödena och de förbättrade flödena:

1. Den fullständiga omdirigeringen ersätts med en ny webbläsarflik där MVPD-inloggningen utförs. Programmeraren krävs för att skapa en ny flik (via `window.open`) namngivna `mvpdwindow` när användaren väljer en MVPD (med `iFrameRequired = false`). Programmeraren körs sedan `setSelectedProvider(<mvpd>)`så att AccessEnabler kan läsa in URL:en för MVPD-inloggning på den nya fliken. När användaren har angett giltiga inloggningsuppgifter stänger Adobe Primetime-autentiseringen fliken och skickar ett window.postMessage till programmerarens webbplats som signalerar till AccessEnabler att autentiseringsflödet har slutförts. Följande återanrop aktiveras:

   - Om flödet initierades av `getAuthentication`: `setAuthenticationStatus` och `sendTrackingData(AUTHENTICATION_DETECTION...)` aktiveras för att signalera lyckad/misslyckad autentisering.

   - Om flödet initierades av `getAuthorization`: `setToken/tokenRequestFailed` och `sendTrackingData(AUTHORIZATION_DETECTION...)` aktiveras för att signalera att auktoriseringen lyckades/misslyckades.

1. Flödet för iFrame-/popup-fönstret är i stort sett oförändrat. Skillnaden är att den överordnade sidan inte läses in igen när användaren har angett giltiga inloggningsuppgifter. iFrame/popup stängs automatiskt efter inloggning och en `window.postMessage` skickas till den överordnade sidan och meddelar AccessEnabler om att flödet har slutförts. Samma återanrop utlöses som i föregående flöde, **plus följande nya återanrop: `destroyIFrame`**. The `destroyIFrame` återanrop gör att programmeraren kan ta bort alla iFrame-associerade/hjälpkomponenter, till exempel UI-dekorationer. Återanropet krävdes inte i det gamla autentiseringsflödet eftersom Adobe Primetime-autentiseringen skulle läsa in programmerarens sida på nytt när inloggningen var klar, vilket innebär att alla gränssnittskomponenter på den förstördes.

</br>     

>[!IMPORTANT]
> 
>Du måste läsa in iFrame- eller popup-fönstret för MVPD-inloggningen som ett direkt underordnat objekt till sidan som innehåller AccessEnabler-instansen. Om iFrame- eller popup-fönstret för MVPD-inloggning är kapslat två eller flera nivåer nedanför sidan med AccessEnabler-instansen kan flödet krascha. Om du till exempel har en iFrame mellan huvudsidan och MVPD iFrame (Page =\> iFrame =\> MVPD iFrame) kan inloggningsflödet misslyckas.

</br>

 **Avbryt autentisering**

Detta är flödena för att avbryta autentisering:

1. **Fliken Webbläsare -** Eftersom fliken i princip är ett nytt fönster har hämtning av close-händelsen samma begränsningar som i scenario 3 från de gamla autentiseringsflödena. Dessutom går det inte att använda den här tidsinställningen eftersom det inte går att skilja mellan en flik som stängdes manuellt av användaren och en flik som stängdes automatiskt i slutet av inloggningsflödet. Lösningen här är att AccessEnabler förblir tyst (inga återanrop aktiveras) när användaren avbryter flödet. Programmeraren behöver inte heller utföra någon specifik åtgärd. Användaren kan initiera ett annat autentiseringsflöde utan att få felmeddelandet &quot;Multiple Authentication Requests Error&quot; (det här felet har inaktiverats i AccessEnabler för bakgrundsinloggning).

1. **iFrame -** Programmeraren kan använda det tillvägagångssätt som beskrivs i scenario 2 från de gamla autentiseringsflödena (skapa omslutningsgränssnitt från iFrame och tillhörande stängningsknapp som utlöser `setSelectedProvider(null)`. Även om detta tillvägagångssätt inte längre är ett starkt krav (flera autentiseringsflöden tillåts för bakgrundsinloggning, vilket beskrivs i scenario 1 ovan), rekommenderas det fortfarande av Adobe.

1. **Popup -** Detta är identiskt med flikflödet ovan.

</br>

## Förbättrat utloggningsflöde {#improved_logout}

Det nya utloggningsflödet utförs i en dold iFrame, vilket eliminerar omdirigeringen av hela sidan.  Detta är möjligt eftersom användaren inte behöver utföra någon specifik åtgärd på MVPD:s utloggningssida.

När utloggningsflödet är klart dirigeras iFrame om till en anpassad Adobe Primetime-autentiseringsslutpunkt. Detta genererar ett JS-fragment som utför en `window.postMessage` till den överordnade och meddela AccessEnabler att utloggningen är klar. Följande återanrop aktiveras: `setAuthenticationStatus()` och `sendTrackingData(AUTHENTICATION_DETECTION ...)`, vilket signalerar att användaren inte längre är autentiserad. 

Bilden nedan visar det uppdateringsfria flödet som gör att en användare kan logga in på sitt MVPD-program utan att uppdatera programmets huvudsida:

**Förbättrad (utan uppdatering) autentisering/utloggningsflöde**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## TempPass-flöde {#improved_temppas}

Inloggning utan uppdatering följer ett annat tillvägagångssätt för MVPD-program av typen TempPass.

Eftersom TempPass-flödet kräver att ett fönster skapas automatiskt och stängs utan någon explicit användarinteraktion, kan det utgöra ett problem för vissa webbläsare (popup-blockerare). AccessEnabler implementerar därför inloggningsfasen bakom scenerna, utan att det krävs en webbbehållare som har skapats av Programmer.

Här är de aspekter som programmeraren måste vara medveten om när TempPass implementeras för uppdatering utan inloggning och inloggning:

- Innan autentiseringen startas behöver iFrame- eller popup-fönstret bara skapas för icke-TempPass MVPD-filer. Programmeraren kan identifiera om ett MVPD är TempPass eller inte genom att läsa `tempPass` MVPD-objektets egenskap (returneras av `setConfig()` / `displayProviderDialog()`).

- The `createIFrame()` callback-funktionen måste innehålla en kontroll för TempPass och dess logik ska bara köras när MVPD är NOT TempPass.

- The `destroyIFrame()` callback-funktionen måste innehålla en kontroll för TempPass och dess logik ska bara köras när MVPD är NOT TempPass.

- The `setAuthenticationStatus()` och `sendTrackingData()` återanrop anropas när autentiseringen har slutförts (exakt som i det uppdateringsfria flödet för vanliga MVPD-program).

>[!NOTE]
>
>Det här flödet är bara tillgängligt för TempPass utan uppdatering. TempPass måste hanteras explicit för uppdateringsflödet (när TempPass kräver iFrame / popup)

</br>

I följande kodexempel visas hur du hanterar ett MVPD-fönster på en programmerares webbplats (både för vanliga MVPD-program och för TempPass):

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```
