---
title: JavaScript SDK - översikt
description: JavaScript SDK - översikt
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# JavaScript SDK - översikt {#javascript-sdk-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion

Adobe rekommenderar att du migrerar till den senaste JS v4.x-versionen av AccessEnabler-biblioteket.

Adobe Primetime JavaScript-integration för autentisering erbjuder programmerare en TV-Everywhere-lösning i den välbekanta utvecklingsmiljön för JS-webbapplikationer. De viktigaste komponenterna i integreringen är ditt&quot;högnivåprogram&quot; (användarinteraktion, videopresentation) och det lågnivåbibliotek för AccessEnabler som Adobe tillhandahåller som ger dig tillgång till tillståndsflödena samt hanterar kommunikationen med Adobe Primetime autentiseringsservrar.

Det allmänna tillståndsflödet för Adobe Primetime-autentisering beskrivs i [Tillståndsflöde för programmerare](/help/authentication/entitlement-flow.md)och JavaScript Integration Cookbook guidar dig genom implementeringen. I följande avsnitt finns beskrivningar och exempel som är specifika för JavaScript AccessEnabler-integreringen.

>[!IMPORTANT]
>
>I det här dokumentet beskrivs implementeringen av en stationär webblösning. JavaScript-biblioteket stöds inte på mobilplattformar (till exempel Safari på iOS, Chrome på Android). Använd våra SDK:er om du vill ha en mobilplattform (iOS, Android, Windows) som mål.

## Skapa dialogrutan för MVPD-val {#creating-the-mvpd-selection-dialog}

För att en användare ska kunna logga in på sitt MVPD och bli autentiserad måste sidan eller spelaren kunna identifiera sitt MVPD-program på ett sätt som användaren kan använda. En standardversion av en dialogruta för MVPD-val tillhandahålls för utveckling. För produktion måste du implementera en egen MVPD-väljare. 

Om du redan vet vem som är kundens leverantör kan du [ställa in MVPD programmatiskt](/help/authentication/home.md), utan användarinteraktion. Tekniken är densamma, men kringgår steget att anropa dialogrutan Leverantörsväljare och be kunden att välja sitt MVPD-program.

## Visa tjänsteleverantören {#displaying-the-service-provider}

I följande kodexempel visas hur du identifierar och visar tjänsteleverantören för den aktuella kunden:

 **HTML** - Den här sidan lägger till ett avsnitt på sidan som visar kundens valda leverantör, om de redan är inloggade:

```HTML
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
            "http://www.w3.org/TR/html4/loose.dtd"> 
    <html>
    <head>
        <title>Get the distributor that is used for the authentication</title>
        <script type="text/javascript" src="libs/jquery-1.4.4.min.js"></script>
        <script type="text/javascript" src="libs/swfobject.js"></script>
        <script type="text/javascript" src="scripts/sample6.js"></script>
    </head>
    <body>
        <div id="alternative">
        <a href="http://www.adobe.com/go/getflashplayer"> 
            <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" 
                 alt="Get Adobe Flash player"/> </a>
        </div> 
        <div id="user_authenticated">Please wait while we verify your authentication status</div> 
        <div id="control">
        <button id="sign_in" style="display:none;">Sign in</button>
        <button id="sign_out" style="display:none;">Sign out</button>
        </div> 
        <div id="distributor"></div> 
        <div id="provider_selector" style="display:none;">
        <select id="provider_list"></select>
        <button id="login">Login</button>
        <button id="cancel">Cancel</button>
        </div> 
        <div id="video_player">This is a video player showing an image as a preview.  You are not yet authorized to see this content.  Make sure that you first sign in.
        </div> 
        <div id="get_authorization">
        <button id="request_access" style="display:none;">Request access</button>
        </div> 
    </body>
    </html>
```
 

**JavaScript** Den här JavaScript-filen frågar om Access Enabler för den aktuella providern är inloggad och visar resultatet i det reserverade sidavsnittet. Den implementerar även en dialogruta för MVPD-väljare:

```JS
    $(function() {
        embedAE();
    }); 
    function embedAE() {
        var flashvars = {};
        var params = {
            bgcolor: "#869ca7",
            quality: "high",
            allowscriptaccess: "always"
        };
        var attributes = {
            id: "ae_swf",
            align: "middle",
            name: "ae_swf"
        };
        swfobject.embedSWF(
                "https://entitlement.auth-staging.adobe.com/entitlement/AccessEnabler.swf",      
                "alternative", "1", "1", "10.1.53", "", flashvars, params, attributes);
    } 
    function getAE() {
        return document.getElementById("ae_swf");
    } 
    function swfLoaded() {
        var swf = getAE();
        initBindings();
        // don't load the default provider-selection dialog 
        swf.setProviderDialogURL("none");
        // identify yourself 
        swf.setRequestor("sample_requestor_Id");
        swf.checkAuthentication();
    } 
    // Define the button actions for the provider dialog
    function initBindings() {
        var provider_selector = $('#provider_selector');
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var login = $('#login');
        var cancel = $('#cancel');
        var request_access = $('#request_access'); 
        sign_out.click(function() {
            getAE().logout();
        });
        sign_in.click(function() {
            getAE().getAuthentication();
        }); 
        login.click(function() {
            var selected_mvpd_id = $("#provider_list option:selected").val();
            getAE().setSelectedProvider(selected_mvpd_id);
        }); 
        cancel.click(function() {
            getAE().setSelectedProvider(null);
            provider_selector.hide();
        }); 
        request_access.click(function(){
            getAE().getAuthorization("sample_requestor_Id");
        });
    }
    // Called if user is already authenticated; queries AE to find the current user's MVPD, 
    // Adds the result to the UI 
    function setDistributor() {
        var distributor = $("#distributor");
        var selectedProvider = getAE().getSelectedProvider();
        distributor.replaceWith('<div id="distributor">' +
                                'Courtesy of ' +
                                selectedProvider.MVPD +
                                '</div>');
    } 
    // Adjust the contents of the provider dialog, based on authentication status 
    // Adds the call to check and display the current distributor, if the user is already
    // logged in. 
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        var user_authenticated = $("#user_authenticated");
        var video_player = $("#video_player");
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var request_access = $('#request_access'); 
        if (isAuthenticated == 1) {
            setDistributor();
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are authenticated - if you wish you can sign out
                                           </div>');
            sign_out.show();
            sign_in.hide();
            video_player.replaceWith('<div id="video_player">Now you can ask for access.</div>');
            request_access.show();
        } else {
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are not authenticated please sign in
                                           </div>');
            sign_in.show();
            sign_out.hide();
        }
    } 
    // Allow user to choose a provider 
    function displayProviderDialog(providers) {
        var provider_list = $("#provider_list");
        var options = provider_list.attr('options');
        for (var index in providers) {
            options[index] = new Option(providers[index].displayName,
                                        providers[index].ID);
        }
        //select the first one by default 
        if (!$("#provider_list option:selected").length)
            $("#provider_list option[0]").attr('selected', 'selected'); 
        $('#provider_selector').show();
    } 
    // Handle the authorization response by sending token to video player 
    function setToken(requested_resource_id, token) {
        var video_player = $("#video_player");
        var request_access = $("#request_access");
        video_player.replaceWith('<div id="video_player">Now you are authorized to ' +
                                 requested_resource_id +
                                 ' content with ' + token + ' . </div>');
    }
```

## Loggar ut {#logout}

Utlysning `logout()` för att initiera utloggningsprocessen. Den här metoden tar inga argument. Den loggar ut den aktuella användaren, rensar all autentiserings- och auktoriseringsinformation för den användaren och tar bort alla AuthN- och AuthZ-token från det lokala systemet.

Det finns vissa fall där spelaren inte ansvarar för att hantera användarutloggningar:

 

- **När utloggningen initieras från en webbplats som inte är integrerad med Adobe Primetime-autentisering.** I det här fallet kan MVPD anropa tjänsten Adobe Primetime authentication Single Logout via en omdirigering till webbläsaren. (Anrop av SLO via ett anrop i bakkanalen stöds inte för närvarande.)

>[!NOTE]
>
>Om användaren lämnar sin dator inaktiv tillräckligt länge så att deras token upphör att gälla, kan de fortfarande återgå till sin session och initiera utloggningen. Adobe Primetime-autentisering säkerställer att alla tokens tas bort och meddelar även MVPD om att ta bort deras session.

I följande JavaScript-kod visas hur du loggar ut (avautentiserar) en autentiserad användare:

```JS
    [...]
    /*
     * @param isAuthenticated authentication status: 1 - Authenticated, 0 - not authenticated 
     * @param errorCode Any error that occurred when determining the authentication status.
     * An empty string if no error occurred.
     */
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        if (isAuthenticated == 1 ) {
            /* User is authenticated – we can logout / deauthenticate */
            accessEnablerObject.logout();
            /* Logs out the current user, clearing all authentication
             * and authorization information for that user. Deletes
             * all authN and authZ tokens from the user's system.
             */
        } else {
            /*
             * User is NOT authenticated – we do not need to logout;
             * Show the log-in image/button/message
             */
        }
    }
```

<!--
**Related Information**

- [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
- [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
- [JavaScript Code Samples](#javascript-code-samples)
- [Understanding Tokens](#understanding_tokens)
-->