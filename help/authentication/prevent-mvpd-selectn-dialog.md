---
title: Förhindra att PDF-filer visas i dialogrutan Markering
description: Förhindra att PDF-filer visas i dialogrutan Markering
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Förhindra att PDF-filer visas i dialogrutan Markering

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Problem {#issue-prevent-mvpd-sel-dialog}

Du måste förhindra att specifika MVPD-filer (&quot;blocklist&quot;) visas i MVPD-väljaren.


## Lösning {#solution-prevent-mvpd-sel-dialog}

Lösningen är att göra en blocklista när `displayProviderDialog()` anropas.

Om du till exempel inte vill att CableCompany_1 och CableCompany_2 ska visas i MVPD-väljaren gör du något liknande som i följande exempel.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```

<!--
**Related Information**

* [Allow MVPDs in the Selection Dialog](/help/authentication/allow-mvpd-selectn-dialog.md)
* **Code samples**
* [Programmer integration guide](/help/authentication/programmer-integration-guide-overview.md)
-->