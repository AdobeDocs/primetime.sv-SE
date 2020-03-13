---
description: Du kan ställa in referensimplementeringen så att den använder Adobe Analytics-rapporter.
seo-description: Du kan ställa in referensimplementeringen så att den använder Adobe Analytics-rapporter.
seo-title: Konfigurera Adobe Analytics-rapportering
title: Konfigurera Adobe Analytics-rapportering
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Konfigurera Adobe Analytics-rapportering {#configure-adobe-analytics-reporting}

Du kan ställa in referensimplementeringen så att den använder Adobe Analytics-rapporter.

Referensimplementeringen är konfigurerad för att skicka händelsedata för autentisering av Primetime till Adobe Analytics med hjälp av Adobe Mobile Library som paketerats i Primetime SDK. Om du vill aktivera och använda händelsedata som skickas från programmet måste du först skapa ett Adobe Analytics-konto. När kontot har skapats:

1. Konfigurera programmet med din kontoinformation; och
1. Skapa bearbetningsregler för att anpassa hur händelsedata visas i dina rapporter.

Tabellen nedan visar de data som skickas till Adobe Analytics:

| Åtgärdsnamn | `a.media.pass.event.MvpdSelection` | Användaren valde en distributör av flerkanalsvideo (MVPD) i en valdialogruta |
|---|---|---|
| Kontextdata | `a.media.pass.MvpdId (String)` | Användarvalt MVPD |
|  | `a.media.pass.ClientType` | (String) Klienttypen är antingen &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; eller &quot;android&quot; |
|  |  |  |
| Åtgärdsnamn | `a.media.pass.event.AuthenticationDetection` | Ett autentiseringsarbetsflöde har slutförts |
| Kontextdata | `a.media.pass.Successful` | (Boolean) Om tokenbegäran lyckades, var true eller false |
|  | `a.media.pass.MvpdId` | (String) Användarvalt MVPD |
|  | `a.media.pass.Guid` | (Sträng) Ett spårnings-ID |
|  | `a.media.pass.Cached` | (Boolean) Token finns redan i cache, true eller false |
|  | `a.media.pass.ClientType` | (String) Klienttypen är antingen &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; eller &quot;android&quot; |
|  |  |  |
| Åtgärdsnamn | `a.media.pass.event.AuthorizationDetection` | Ett auktoriseringsarbetsflöde har slutförts |
| Kontextdata | `a.media.pass.Successful` | (Boolean) Om tokenbegäran lyckades, var true eller false |
|  | `a.media.pass.MvpdId` | (String) Användaren har valt MVPD |
|  | `a.media.pass.Guid` | (Sträng) Ett spårnings-ID |
|  | `a.media.pass.Cached` | (Boolean) Token finns redan i cache, true eller false |
|  | `a.media.pass.Error` | (String) Felet om auktoriseringsförsöket misslyckades |
|  | `a.media.pass.ErrorDetails` | (String) Ytterligare felinformation |
|  | `a.media.pass.ClientType` | (String) Klienttypen är antingen &quot;flash&quot;, &quot;html5&quot;, &quot;ios&quot; eller &quot;android&quot; |

1. Konfigurera programmet för användning med Adobe Marketing Cloud.

   Om du vill aktivera sändning av Primetime Primetime-autentiseringsdata till Adobe Analytics, måste en konfigurationsfil läggas till i referensimplementeringen vid kompileringen [!DNL `ADBMobileConfig.json`] . Observera att detta är exakt samma konfigurationsfil som används av Primetime SDK för att skicka videoanalysdata till Marketing Cloud. Mer information om hur du konfigurerar ett program med ditt Adobe Analytics-konto finns i dokumentationen [för](https://microsite.omniture.com/t2/help/en_US/reference/) Adobe Marketing Cloud.
1. Skapa bearbetningsregler.

   De händelsedata för autentisering av Primetime som skickas av referensimplementeringen visas inte automatiskt i dina analysrapporter. Du måste först använda data genom att skapa bearbetningsregler. Läs [Adobe Analytics-dokumentationen om hur du skapar bearbetningsregler](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
