---
title: Migrera inloggningssidan för MVPD från iFrame till Popup
description: Migrera inloggningssidan för MVPD från iFrame till Popup
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Migrera inloggningssidan för MVPD från iFrame till Popup {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Popup kontra iFrame {#popup-vs-iframe}

Vissa användare har stött på cookie-problem från tredje part med iFrame-implementeringen av en MVPD-inloggningssida.
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

Adobe Primetime autentiseringsteam **rekommenderar att inloggningssidan för popup-fönster implementeras** i stället för iFrame-versionen i Firefox och Safari.  Om du implementerar en inloggningssida för Internet Explorer kan du stöta på problem med popup-implementeringen. IE-problemen orsakas av att Adobe Primetime-autentiseringen tvingar en överordnad sida att omdirigeras efter att användaren har autentiserat med sitt MVPD i popup-fönstret, vilket ses som en popup-blockerare i Internet Explorer. Adobe Primetime autentiseringsteam **rekommenderar att iFrame-inloggningen för Internet Explorer implementeras**.

I exempelkoden i den här TechNote-artikeln används en hybridimplementering av både iFrame och popup-fönster, som öppnar en iFrame i Internet Explorer och ett popup-fönster i andra webbläsare.

Med tanke på att det redan finns en iFrame-implementering, presenterar den första delen av TechNote koden för iFrame-implementeringen och den andra delen presenterar ändringarna för att få plats med popup-implementeringen som standard.


## MVPD-väljaren med inloggningssida i en iFrame {#mvpd-pickr-iframe}

I tidigare kodexempel visades en HTML-sida som innehåller &lt;div> -tagg där iFrame ska skapas tillsammans med knappen close för iFrame:

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

Här är de associerade **JavaScript** kod:

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}
```


## MVPD-väljaren med inloggningssida i ett popup-fönster {#mvpd-pickr-popup}

Eftersom vi inte använder en **iFrame** HTML-koden innehåller inte längre iFrame eller den knapp som behövs för att stänga iFrame. Den div som tidigare innehöll iFrame - **mvpddiv** - kommer att förvaras och användas för följande:

* för att meddela användaren att inloggningssidan för MVPD redan är öppen om popup-fokus försvinner
* för att skapa en länk för att återfå fokus på popup-fönstret

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

Listan över MVPD visas i den div som anropas **väljare** som ett val **-mvpdList**.

Ett nytt API-återanrop används - **setConfig(configXML)**. Återanropet aktiveras efter att funktionen setRequestor(requestID) har anropats. Det här återanropet returnerar en lista över MVPD-filer som är integrerade med det beställar-ID som tidigare angetts. I callback-metoden tolkas den inkommande XML-filen och listan över MVPD-filer cachelagras. MVPD-väljaren skapas också men visas inte.

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

När funktionen getAuthentication() eller getAuthorization() har anropats aktiveras callback-funktionen displayProviderDialog(). I det här återanropet hade MVPD-listan normalt byggts och visats. Eftersom MVPD-väljaren redan är byggd är det enda som återstår att göra att visa den för användaren.

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

När användaren har valt ett PDF-dokument i väljaren måste popup-fönstret skapas. Vissa webbläsare kan blockera popup-fönstret om det skapas med about:blank eller med en sida som finns i en annan domän. Därför bör du öppna det med värdnamnet som AccessEnabler läses in från.

I iFrame-implementeringen återställs autentiseringsflödet av knappen btnCloseIframe och JavaScript-funktionen closeIframeAction(), men nu går det inte längre att dekorera iFrame. Så samma beteende uppnås genom att man tittar efter när popup-fönstret stängs (antingen av användaren eller genom att autentiseringsflödet slutförs). Ett kodfragment har lagts till som också är användbart om användaren förlorar fokus i popup-fönstret:

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

I återanropet createIFrame() visas **mvpddiv** div visas.

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* Exempelkoden innehåller en hårdkodad variabel för det begärda begärorID:t - REF, som ska ersättas med ett riktigt programmerarbegärande-ID.
>* Exempelkoden kommer endast att köras korrekt från en vitlistad domän som är associerad med det begärande-ID som används.
>* Eftersom hela koden är tillgänglig för hämtning har koden som presenteras i den här TechNote trunkerats. Ett fullständigt exempel finns på **JS iFrame vs Popup Sample**.
>* De externa JavaScript-biblioteken länkades från [Google värdtjänster](https://developers.google.com/speed/libraries/).
