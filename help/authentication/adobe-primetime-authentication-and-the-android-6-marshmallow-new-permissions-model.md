---
title: Adobe Primetime Authentication and the Android 6 "Marshmallow" New Permissions Model
description: Adobe Primetime Authentication and the Android 6 "Marshmallow" New Permissions Model
exl-id: 3c96769e-b25b-48ab-bb74-40f13d4e5a84
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Adobe Primetime Authentication and the Android 6 &quot;Marshmallow&quot; New Permissions Model {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>

I den nya Marshmallow-versionen för Android 6 introduceras vissa uppdateringar av behörighetsmodellen, vilket kan påverka beteendet för appar som använder den befintliga SDK-autentiseringsversionen av Adobe Primetime version 1.8 och äldre.

Det nya operativsystemet Android erbjuder en ny funktion [detaljkontroll över de behörigheter som krävs för appar vid installation och körning](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>Ändringarna som beskrivs nedan **påverkar bara program som utvecklats specifikt för Android 6.0** (targetSdkVersion=23). De påverkar inte äldre program som redan är installerade på användarens enhet vid uppgradering till Android 6.0.


För program som utvecklats i Android Studio med [API-nivå 23](http://developer.android.com/sdk/api_diff/23/changes.html) och som använder Adobe Primetime Authentication SDK måste utvecklaren skriva egen kod (se kodutdrag nedan) [för att aktivera dialogrutan Tillåt/Neka behörigheter](https://developer.android.com/training/permissions/requesting.html).

Här följer det kodutdrag som används för att begära skrivåtkomst till enhetens externa lagring:

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**Ur användarens perspektiv** Vid installationen visas ett fönster där användaren uppmanas att bekräfta läs- och skrivbehörighet för filer (se figur 2 nedan). Detta leder till ett av följande två resultat:

1. Om användaren **bekräftar** behörigheter, det reguljära autentiseringsflödet behålls och tokens lagras i den globala lagringen. Användare förblir autentiserade i appen och mellan appar med hjälp av Adobe Primetime-autentisering så länge tokenerna är giltiga.
1. Om användaren **förnedrande** behörigheter, skrivåtgärder i lagringsutrymmet misslyckas och användarna autentiseras bara tills de avslutar programmet. Observera att vissa program återinitieras när de växlar mellan förgrund och bakgrund, så att användarna loggas ut när den här åtgärden utförs. Tokens lagras INTE och användarna måste autentisera varje gång de använder appen.


>[!TIP]
>
>En funktion som introducerar lagringsflexibilitet håller på att utvecklas för Adobe Primetime autentisering SDK 1.9. Den nya SDK:n är avsedd för **släppt den sista veckan i oktober**. Programmet återgår till att skriva i programmets sandlådelagring när den allmänna lagringen inte kan användas. Detta omfattar det fall där användare, för program som utvecklats på API-nivå 23, INTE accepterar läs-/skrivbehörigheter i den globala lagringen. Token lagras individuellt per app vilket innebär att enkel inloggning mellan program som använder Adobe Primetime-autentisering inaktiveras.


![](assets/android-permissions-request.png)

*Bild: Dialogrutan för behörighetsbegäran för program som skrivits på API-nivå 23*

>[!IMPORTANT]
>
> Adobe rådgivare **sina partner för att utveckla appar med API-nivå 22 (targetSdkVersion=22) eller äldre för att garantera bästa möjliga användarupplevelse i autentiseringsprocessen**.
